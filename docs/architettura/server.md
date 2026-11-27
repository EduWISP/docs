---
title: Architettura del server
parent: Architettura
nav_order: 5
---

# Architettura del server

Decisioni in [ADR-0016](../decisioni/0016-architettura-del-server.md). Installazione con il ruolo [`ansible-eduwisp`](https://github.com/EduWISP/ansible-eduwisp).

## Stato dell'implementazione

Aggiornato al 27 novembre 2026, su `server.eduwisp.org` ([ambiente demo](https://demo.eduwisp.org), solo dati fittizi).

| Componente | Stato |
|---|---|
| nginx con TLS, header di sicurezza, limiti di richieste | ✅ attivo |
| Django + gunicorn isolato | ✅ attivo |
| PostgreSQL 17 | ✅ attivo |
| Valkey + Celery worker e beat | ✅ attivo |
| Backup BorgBackup e prova di ripristino mensile | ✅ attivo · ⏳ manca l'archivio **remoto** |
| Monit e riepilogo quotidiano di sicurezza | ✅ attivo · ⏳ invio email da verificare |
| Log al massimo 90 giorni | ✅ attivo |
| Firewall, fail2ban, Suricata, AIDE, auditd, hardening | ✅ attivo (Lynis 78/100) |
| Endpoint `/health/` | ⏳ da fare (eduwisp-utils) |
| Autenticazione a più fattori | ⏳ da fare (eduwisp-users) |
| Aggiornamento per rilasci della piattaforma | ⏳ da fare |
| Separazione dei dati di cyberbullismo e Family Control | ⏳ da progettare |

Tutto è installato dal ruolo [`ansible-eduwisp`](https://github.com/EduWISP/ansible-eduwisp), idempotente.

## Componenti

```text
                Internet / rete della scuola
                            │ HTTPS (443)
                ┌───────────▼───────────┐
   firewall ──► │ nginx                 │  TLS, file statici, limite di richieste
   Suricata     └───────────┬───────────┘
   fail2ban                 │ socket Unix
                ┌───────────▼───────────┐
                │ Django + gunicorn     │  interfaccia web e API del protocollo
                └──────┬──────────┬─────┘
                       │          │ attività
                       │   ┌──────▼──────┐   ┌──────────────────┐
                       │   │ Valkey      │◄──┤ Celery beat      │ pianificazione
                       │   │ (solo locale)│   └──────────────────┘
                       │   └──────┬──────┘
                       │   ┌──────▼──────┐
                       │   │ Celery      │ attività in background
                       │   │ worker      │
                       │   └──────┬──────┘
                ┌──────▼──────────▼─────┐
                │ PostgreSQL 17         │  dati della scuola
                │  · schema cyberbullismo separato
                └───────────────────────┘
                ┌───────────────────────┐
                │ PostgreSQL: Family    │  database separato (anche su altro server)
                └───────────────────────┘

   Backup (BorgBackup) ──► archivio remoto cifrato, in sola aggiunta
   Monit + AIDE + auditd + riepiloghi Suricata ──► email agli amministratori
```

| Componente | Ruolo | Utente | Rete |
|---|---|---|---|
| nginx | TLS, statici, proxy, limite di richieste | `www-data` | 80, 443 |
| gunicorn (Django) | interfaccia e API | `eduwisp` | socket Unix |
| Celery worker | attività in background (notifiche, report, pulizie) | `eduwisp` | locale |
| Celery beat | attività pianificate | `eduwisp` | locale |
| Valkey | coda dei messaggi | `valkey` | solo socket locale, con password |
| PostgreSQL 17 | dati | `postgres` | solo socket locale |

## Attività pianificate previste

- scadenza dei token di registrazione e pulizia dei dati temporanei;
- **applicazione dei tempi di conservazione** (cancellazione dei dati oltre il termine, RC-002);
- azzeramento periodico dell'ambiente **demo** (ADR-0015);
- passaggio d'anno guidato (RF-008), su richiesta;
- riepiloghi aggregati per i report.

## Dati

| Dati | Dove | Protezione |
|---|---|---|
| Struttura scolastica, dispositivi, policy, audit | database principale | accesso locale, backup cifrati |
| Cyberbullismo | **schema separato** con ruolo dedicato | campi delicati cifrati a livello applicativo, accesso ristretto e registrato |
| Family Control | **database separato** | separato dalla scuola (ADR-0014) |
| Segreti (chiave Django, password Valkey) | `/etc/eduwisp/` | `root:eduwisp`, permessi `0640` |
| Log | journald | 90 giorni, solo amministratori |

In produzione: **cifratura del disco** a livello di VM o di storage.

## Backup e ripristino

| Cosa | Come | Quando |
|---|---|---|
| Database | `pg_dump` in formato custom | ogni notte |
| Configurazione | `/etc/eduwisp`, `/etc/nginx`, inventario | ogni notte |
| Archivio | **BorgBackup** cifrato, remoto, *append-only* | ogni notte |
| Conservazione | 7 giornalieri, 4 settimanali, 6 mensili | — |
| Prova di ripristino | ripristino automatico in un database temporaneo | ogni mese |

Le cancellazioni (per esempio per diritto all'oblio) si estendono ai backup alla loro naturale scadenza: va indicato nell'informativa. Obiettivo per una scuola: perdita massima di dati **24 ore**, ripristino entro **4 ore**. Per il pilota si valuterà l'archiviazione continua del registro di PostgreSQL (pgBackRest).

## Aggiornamenti

1. **Debian:** patch di sicurezza automatiche; `needrestart` segnala i servizi da riavviare; i riavvii per il kernel si pianificano fuori dall'orario scolastico.
2. **EduWISP:** si aggiorna a un **rilascio della piattaforma**, che fissa le versioni di tutti i moduli. Il ruolo Ansible:
   1. esegue un backup;
   2. ferma Celery;
   3. installa le nuove versioni;
   4. applica le migrazioni e aggiorna i file statici;
   5. riavvia i servizi e verifica l'endpoint di stato.
3. **Ritorno alla versione precedente:** si ripristinano il backup e le versioni precedenti (le migrazioni del database vanno solo in avanti).

## Monitoraggio

- **Endpoint di stato** (`/health/`): applicazione, database, coda.
- **Monit:** servizi attivi, spazio su disco, memoria, scadenza del certificato, risposta dell'endpoint di stato.
- **Sicurezza:** riepilogo quotidiano degli allarmi Suricata, rapporto AIDE, eventi auditd rilevanti, ban di fail2ban.
- **Avvisi via email** tramite relay SMTP della scuola o del fornitore.
- Opzionale per installazioni grandi: Prometheus e Grafana.

## Dimensionamento indicativo

Con l'interrogazione ogni 15 minuti, ogni dispositivo genera in media circa una richiesta ogni 7–8 minuti (policy e stato): 500 dispositivi ≈ 1 richiesta al secondo.

| Dispositivi | Configurazione |
|---|---|
| fino a 500 (un istituto) | 1 VM: 2 vCPU, 4 GB RAM, 40 GB disco |
| fino a 3.000 (rete di istituti) | 1 VM: 4 vCPU, 8 GB RAM, 100 GB SSD |
| fino a 20.000 | VM applicativa (8 vCPU, 16 GB) + VM PostgreSQL dedicata (4 vCPU, 16 GB, SSD) |
| oltre | più istanze applicative dietro un bilanciatore, PostgreSQL con replica |

Suricata richiede circa 0,5–1 GB di RAM in più. **Valori da verificare con prove di carico.**
