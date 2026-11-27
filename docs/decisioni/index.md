---
title: Decisioni (ADR)
nav_order: 7
has_children: true
---

# Registro delle decisioni

Le decisioni progettuali rilevanti sono registrate come **Architecture Decision Record (ADR)**: documenti brevi, numerati e immutabili. Una decisione superata non si cancella: si crea un nuovo ADR che la sostituisce e si aggiorna lo stato del precedente.

| ADR | Titolo | Stato |
|---|---|---|
| [0001](0001-uso-degli-adr.md) | Registrare le decisioni con ADR | Accettata |
| [0002](0002-modello-scuola-famiglia.md) | Modello scuola-famiglia a due ambiti coordinati | Accettata |
| [0003](0003-target-android.md) | Target Android e strada tecnica: DPC EduWISP open source | Proposta |
| [0004](0004-debian-13-server.md) | Debian GNU/Linux 13 come piattaforma server di riferimento | Accettata |
| [0005](0005-cloud-first-self-hostable.md) | Modello di distribuzione cloud-first ma self-hostable | Accettata |
| [0006](0006-licenza.md) | Licenze: AGPL-3.0-or-later con attribuzione per il codice, CC BY-SA 4.0 per i testi, marchio escluso | Accettata |
| [0007](0007-lingue-documentazione.md) | Documentazione bilingue, italiano predefinito | Accettata |
| [0008](0008-conformita-normativa.md) | Conformità normativa come vincolo bloccante | Accettata |
| [0009](0009-solo-software-libero.md) | Solo componenti open source e gratuiti | Accettata |
| [0010](0010-un-repository-per-modulo.md) | Un repository per ogni modulo | Accettata |
| [0011](0011-multipiattaforma.md) | Architettura indipendente dalla piattaforma dei dispositivi | Accettata |
| [0012](0012-responsabile-del-progetto.md) | Responsabile del progetto | Accettata |
| [0013](0013-stack-tecnologico.md) | Stack tecnologico: Django 5.2 LTS, PostgreSQL, Kotlin senza servizi Google | Accettata |
| [0014](0014-family-control-facoltativo-multipiattaforma.md) | Family Control facoltativo e multipiattaforma (Android, Windows, Linux; Apple in programma) | Accettata (principi) |
| [0015](0015-ambienti-del-progetto.md) | Ambienti: server.eduwisp.org, demo con dati fittizi, pilota solo dopo i requisiti legali | Accettata |
| [0016](0016-architettura-del-server.md) | Architettura del server: componenti, dati separati, backup, aggiornamenti, monitoraggio | Accettata |
| [0017](0017-server-di-backup.md) | Server di backup dedicato su Debian stable: Borg in sola aggiunta, cifratura sul client, ruolo Ansible e poi ISO | Accettata |
| [0018](0018-interfaccia-per-ruoli.md) | Interfaccia divisa per ruoli: amministratore di sistema con tutti gli istituti e le impostazioni, dirigente, docente, famiglia; permessi controllati sul server, famiglia con un referente e un secondo facoltativo, selettore di vista in sola lettura; studenti maggiorenni: accesso dei familiari solo con il loro consenso dal tablet | Accettata |
| [0019](0019-app-consentite.md) | App consentite: elenco per istituto, indirizzo e classe, sblocco temporaneo del docente registrato, app non consentite sospese, nessun inventario inviato al server | Accettata |

**Stati:** Proposta · Accettata · Respinta · Sostituita da ADR-XXXX

## Come proporre una decisione

1. Copia il [modello](0000-modello.md) con il numero successivo.
2. Apri una pull request con stato *Proposta* e collega la discussione.
3. Dopo la discussione i maintainer aggiornano lo stato.
