# EduWISP

**Open-source platform for managing school-owned Android devices**

EduWISP è una proposta di piattaforma open source per la gestione dei dispositivi Android di proprietà delle scuole. Ispirato alla modularità e alla filosofia di OpenWISP, il progetto intende unire Mobile Device Management (MDM), gestione scolastica, Family Control e strumenti di prevenzione e gestione del cyberbullismo.

> **Stato: progettazione.** Questo repository contiene documentazione e specifiche concettuali. Non contiene un server MDM funzionante, applicazioni Android o procedure di installazione.

## Visione

Offrire alle scuole una piattaforma aperta, modulare e verificabile per amministrare i tablet didattici, distribuire applicazioni e applicare regole coerenti con il contesto scolastico e familiare, tutelando al contempo la dignità, i diritti e la riservatezza degli studenti.

## Principi

- Open source, modularità e API documentabili.
- Cloud-first, ma installabile autonomamente (self-hosted).
- Nessuna dipendenza obbligatoria da un servizio cloud proprietario per il core.
- Separazione dei dati tra istituti (multi-tenancy).
- Privacy by design e minimizzazione dei dati.
- Supervisione umana per le segnalazioni e gli interventi.
- Trasparenza delle regole e tracciabilità degli accessi amministrativi.

## Aree funzionali

| Area | Scopo |
|---|---|
| Core & Identity | Organizzazioni, utenti, ruoli, autenticazione e autorizzazioni |
| School Management | Istituti, plessi, classi, docenti, studenti e assegnazioni |
| MDM | Inventario, provisioning e gestione dei dispositivi |
| Android Provider | Integrazione con le API e i servizi Android supportati |
| Application Management | Catalogo, assegnazione e configurazione delle app |
| Policy Engine | Composizione e risoluzione delle policy |
| Family Control | Regole familiari coordinate con quelle scolastiche |
| Cyberbullying & Digital Wellbeing | Segnalazioni, prevenzione e gestione degli incidenti |
| Audit & Reporting | Tracciamento delle operazioni e report minimizzati |
| Web Interface & API | Interfacce per i diversi ruoli e integrazioni |

## Family Control: modello concordato

EduWISP adotta come modello progettuale due ambiti di gestione coordinati:

- **Scuola:** mantiene la responsabilità della gestione istituzionale del dispositivo, della sicurezza e delle attività didattiche.
- **Famiglia:** può configurare regole aggiuntive per l'utilizzo domestico e il tempo extrascolastico, nei limiti definiti dal progetto.

Le regole familiari non possono annullare i requisiti di sicurezza né impedire attività didattiche obbligatorie. Le priorità e le eccezioni devono essere esplicite, comprensibili e verificabili.

## Cyberbullying & Digital Wellbeing

Il modulo ha finalità preventive e di supporto, non di sorveglianza indiscriminata. Le funzioni concettuali includono:

- canale di segnalazione accessibile agli studenti;
- segnalazioni da parte di docenti e personale autorizzato;
- gestione riservata dei casi, con accesso ristretto;
- assegnazione di un referente e tracciamento dello stato;
- procedure di presa in carico, tutela e follow-up;
- contenuti di educazione digitale e prevenzione;
- indicatori aggregati di benessere digitale, ove appropriati.

**Fuori perimetro:** lettura generalizzata di chat private, accesso indiscriminato a foto o messaggi, keylogging, sorveglianza occulta, geolocalizzazione continua e classifiche individuali di comportamento. Eventuali strumenti di analisi devono avere finalità specifica, base giuridica verificata, trasparenza, proporzionalità e supervisione umana. Nessun sistema automatico deve decidere sanzioni o qualificare autonomamente uno studente come autore di bullismo.

## Android

Il target iniziale è costituito da tablet Android con Google Mobile Services (GMS), di proprietà degli istituti. La modalità **Fully Managed / Android Enterprise** è un'ipotesi primaria da verificare. L'uso di Android Management API e dei relativi servizi è subordinato ai requisiti e alle condizioni Google: non si presume che qualsiasi progetto possa accedervi automaticamente.

Il core di EduWISP dovrà rimanere logicamente indipendente dal provider MDM. Le funzionalità effettive (kiosk, app management, restrizioni, aggiornamenti, telemetria) dovranno essere validate rispetto alle API e ai dispositivi supportati.

## Hosting e piattaforma server

- Approccio: cloud-first, self-hosted supportato.
- Sistema operativo di riferimento per il server: **Debian GNU/Linux 13 (Trixie)**.
- La scelta di servizi, database, runtime e modalità di packaging resta da validare nella progettazione tecnica.
- Il requisito Debian riguarda la piattaforma server; non implica che ogni container debba necessariamente usare Debian come base.

## Documentazione

- [Visione e perimetro](docs/vision.md)
- [Requisiti](docs/requirements.md)
- [Architettura concettuale](docs/architecture.md)
- [Gestione Android](docs/android-management.md)
- [MDM](docs/mdm.md)
- [Gestione scolastica](docs/school-management.md)
- [Family Control](docs/family-control.md)
- [Policy Engine](docs/policy-engine.md)
- [Cyberbullismo e benessere digitale](docs/cyberbullying-wellbeing.md)
- [Sicurezza](docs/security.md)
- [Privacy e conformità](docs/privacy.md)
- [Deployment concettuale](docs/deployment.md)
- [Governance](docs/governance.md)
- [Roadmap](docs/roadmap.md)

## Stato e contributi

La fase corrente è esclusivamente progettuale. Sono benvenuti contributi alla definizione dei requisiti, all'analisi delle API Android, alla privacy, alla sicurezza e alla documentazione. Le modalità formali di contribuzione saranno definite nella governance.

## Licenza

La licenza non è ancora stata scelta. AGPL-3.0 è un'opzione da valutare, non una decisione già assunta. Non applicare una licenza al progetto prima della relativa decisione.
