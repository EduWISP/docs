---
title: "ADR-0016: Architettura del server"
parent: Decisioni (ADR)
nav_order: 16
---

# ADR-0016: Architettura del server

- **Stato:** Proposta
- **Data:** 2026-11-27

## Contesto

Il ruolo `ansible-eduwisp` installa già applicazione, database, web e sicurezza ([ADR-0015](0015-ambienti-del-progetto.md)). Mancano le decisioni su attività in background, separazione dei dati, backup, aggiornamenti, monitoraggio e dimensionamento. Vanno prese **prima** della ISO di installazione, che impacchetterà questa architettura. La descrizione completa è nella pagina [Architettura del server](../architettura/server.md).

## Decisione proposta

1. **Un solo server di partenza, pronto a crescere.** Tutti i componenti stanno su un'unica VM Debian 13. L'applicazione non conserva stato in memoria, così in futuro si possono aggiungere istanze e separare il database senza riscriverla.
2. **Componenti:** nginx (TLS, file statici, limite di richieste sulle API), Django con gunicorn (interfaccia e API), PostgreSQL 17 (unica fonte dei dati), **Valkey** (coda dei messaggi, raggiungibile solo in locale), **Celery** worker e Celery beat (attività in background e pianificate). Ogni servizio gira come utente dedicato con l'isolamento di systemd.
3. **Separazione dei dati:**
   - i dati del **Family Control** stanno in un **database separato** ([ADR-0014](0014-family-control-facoltativo-multipiattaforma.md)), installabile anche su un altro server;
   - i dati del **cyberbullismo** stanno in uno **schema PostgreSQL separato**, con un ruolo del database dedicato e i campi più delicati cifrati a livello applicativo;
   - in produzione si consiglia la cifratura del disco (a livello di VM o di storage).
4. **Backup con BorgBackup:** dump notturno del database e copia della configurazione, cifrati, verso un archivio **remoto in sola aggiunta** (protetto da cancellazioni e ransomware). Conservazione: 7 giornalieri, 4 settimanali, 6 mensili. **Prova di ripristino automatica** ogni mese. Gli snapshot della VM (per esempio Proxmox Backup Server) completano i backup ma non li sostituiscono.
5. **Aggiornamenti:**
   - Debian: patch di sicurezza automatiche (già attive); riavvii per il kernel pianificati fuori dall'orario scolastico;
   - EduWISP: le versioni dei moduli sono fissate da un **rilascio della piattaforma** ([ADR-0010](0010-un-repository-per-modulo.md)); l'aggiornamento con Ansible fa prima un backup, poi installa, applica le migrazioni e verifica lo stato. Per tornare indietro si ripristina il backup.
6. **Monitoraggio e log:**
   - in ogni installazione: endpoint di **stato** dell'applicazione, **Monit** per servizi, disco, certificati e memoria, riepiloghi quotidiani di **Suricata** e **AIDE**, avvisi via email tramite un relay SMTP;
   - log in journald con conservazione di **90 giorni** e accesso solo agli amministratori (contengono indirizzi IP e identificativi);
   - per installazioni grandi, opzionale: Prometheus e Grafana.
7. **Sicurezza applicativa aggiuntiva:** limite di richieste sulla registrazione dei dispositivi, autenticazione a più fattori per gli amministratori.
8. **Dimensionamento** indicativo nella pagina dedicata, da verificare con prove di carico.

## Alternative considerate

- **Microservizi o Kubernetes dall'inizio:** troppo complessi per una scuola che installa in proprio (ADR-0005, ADR-0010).
- **restic** invece di BorgBackup: equivalente e anch'esso libero; Borg è preferito per la modalità *append-only* e la maturità in Debian.
- **Prometheus e Grafana in ogni installazione:** troppo pesanti per un piccolo istituto; restano un'opzione.

## Conseguenze

- Il ruolo `ansible-eduwisp` va completato con Valkey e Celery, backup, Monit con relay SMTP, limiti di richieste e conservazione dei log.
- I moduli devono fornire l'endpoint di stato (in `eduwisp-utils`) e l'autenticazione a più fattori (in `eduwisp-users`).
- La ISO di installazione si costruirà su questa architettura.
