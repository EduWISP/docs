---
title: "ADR-0015: Ambienti del progetto"
parent: Decisioni (ADR)
nav_order: 15
---

# ADR-0015: Ambienti del progetto

- **Stato:** Accettata
- **Data:** 2026-11-27

## Contesto

Il progetto ha acquistato il dominio **eduwisp.org** e dispone di una macchina virtuale su Proxmox. Serve un ambiente in cui le scuole possano provare EduWISP, senza mettere a rischio dati di minori ([ADR-0008](0008-conformita-normativa.md), RC-001).

## Decisione

### Nomi

- **Le macchine hanno nomi neutri, i servizi hanno nomi funzionali.** I servizi puntano alle macchine con record DNS, così si possono spostare senza cambiare indirizzo.
- Prima macchina: **`server.eduwisp.org`** (VM `eduwisp-server` su Proxmox, Debian 13, [ADR-0004](0004-debian-13-server.md)).
- Tutti i servizi del progetto stanno sotto **eduwisp.org**. Altri domini eventualmente registrati (per esempio `.it`) reindirizzano a `eduwisp.org`.
- Le installazioni delle scuole o dei fornitori **non** usano `eduwisp.org`: ognuno usa il proprio dominio (modello self-hosted, [ADR-0005](0005-cloud-first-self-hostable.md)).

### Ambienti

| Ambiente | Indirizzo | Dati | Quando |
|---|---|---|---|
| **Sito e documentazione** | `eduwisp.org`, `eduwisp.org/docs/` | Nessun dato personale | Ora |
| **Demo** | `demo.eduwisp.org` → `server.eduwisp.org` | **Solo dati fittizi** | Ora |
| **Pilota** | `pilota.eduwisp.org` | Dati reali di scuole aderenti | Solo dopo i requisiti sotto |

**Demo:**
- ogni scuola che vuole provare ha il proprio istituto (tenant), con classi, studenti e docenti **inventati**;
- solo **dispositivi di prova**, mai quelli in uso agli studenti;
- avviso sempre visibile: «Ambiente di prova: non inserire dati reali»;
- dati **azzerati periodicamente**, nessuna garanzia di disponibilità;
- account delle scuole creati su richiesta, con autenticazione a più fattori per gli amministratori.

**Pilota:** si attiva solo quando sono soddisfatti tutti questi requisiti:
1. DPIA e revisione legale completate (ADR-0008, RC-001);
2. un **soggetto giuridico** del progetto (per esempio un'associazione) che possa firmare gli accordi;
3. **accordo di responsabile del trattamento** (GDPR art. 28) con ogni scuola aderente;
4. per le scuole statali, verifica della **qualificazione cloud ACN** richiesta;
5. hosting **nell'Unione europea** presso un fornitore con disponibilità, backup e sicurezza adeguati; la connessione domestica non è adatta;
6. procedure documentate di backup, ripristino, gestione degli incidenti e cancellazione dei dati.

## Alternative considerate

- **Pilota subito con dati reali sulla VM del progetto:** escluso, perché violerebbe RC-001 e non garantirebbe la sicurezza dovuta ai dati di minori.
- **Nessun ambiente condiviso, solo installazioni locali:** più sicuro, ma impedirebbe alle scuole di provare il progetto senza competenze tecniche.

## Conseguenze

- Il ruolo `ansible-eduwisp` viene sviluppato installando proprio `server.eduwisp.org`.
- L'interfaccia deve prevedere un **avviso di ambiente di prova** configurabile.
- Il soggetto giuridico del progetto diventa un prerequisito anche per il pilota (oltre che per il marchio).
