---
title: Home
nav_order: 1
permalink: /
---

# EduWISP
{: .fs-9 }

Piattaforma open source per la gestione dei dispositivi Android di proprietà delle scuole.
{: .fs-6 .fw-300 }

[Leggi la visione](progetto/visione.md){: .btn .btn-primary .mr-2 }
[Partecipa alla discussione](https://github.com/EduWISP/docs/discussions){: .btn .mr-2 }
[English](/docs/en/){: .btn }

---

{: .warning }
> **Stato: progettazione.** Questa documentazione descrive una progettazione in corso. Non esiste ancora un prodotto funzionante e non vengono fornite istruzioni di installazione.

## Cos'è EduWISP

EduWISP è una proposta di piattaforma open source che unisce **Mobile Device Management (MDM)**, **gestione scolastica**, **Family Control** e strumenti di **prevenzione del cyberbullismo**, ispirandosi alla modularità e alla filosofia di [OpenWISP](https://openwisp.org/).

## Come è organizzata la documentazione

| Sezione | Contenuto |
|---|---|
| [Progetto](progetto/index.md) | Visione, perimetro, roadmap, governance, glossario |
| [Requisiti](requisiti/index.md) | Requisiti funzionali e non funzionali, con stato di approvazione |
| [Architettura](architettura/index.md) | Domini logici, Policy Engine, deployment |
| [Moduli](moduli/index.md) | MDM, Android, gestione scolastica, Family Control, cyberbullismo |
| [Sicurezza e privacy](sicurezza-privacy/index.md) | Principi di sicurezza, threat model, privacy e GDPR |
| [Decisioni (ADR)](decisioni/index.md) | Registro delle decisioni progettuali |

## Principi in breve

- **Open source**, modulare, con API documentate.
- **Cloud-first ma self-hostable**: nessuna dipendenza obbligatoria da un cloud proprietario.
- **Multi-tenancy**: dati separati tra istituti.
- **Privacy by design**: minimizzazione dei dati, nessuna sorveglianza degli studenti.
- **Supervisione umana** per segnalazioni e interventi.
- **Trasparenza** delle regole e tracciabilità delle operazioni amministrative.

## Modello scuola-famiglia

La scuola mantiene il governo istituzionale del dispositivo. La famiglia può applicare regole aggiuntive nel contesto domestico, senza poter disattivare le policy di sicurezza o impedire le attività didattiche obbligatorie. Vedi [ADR-0002](decisioni/0002-modello-scuola-famiglia.md).

## Lingue

La documentazione è in **italiano** (versione di riferimento) e in **inglese**. In caso di differenze prevale la versione italiana.
