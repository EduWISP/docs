---
title: Requisiti funzionali e non funzionali
parent: Requisiti
nav_order: 1
---

# Requisiti

I requisiti seguenti sono una baseline progettuale da discutere e validare. Non descrivono funzionalità già implementate.

**Stato:** `proposto` · `approvato` · `respinto` · `sospeso`. Per proporre o modificare un requisito apri una issue con il modello **Requisito**.

## Requisiti funzionali

### Organizzazioni e identità

| ID | Requisito | Modulo | Stato |
|---|---|---|---|
| RF-001 | Supportare più istituti con separazione logica dei dati. | Core | proposto |
| RF-002 | Gestire ruoli e permessi granulari. | Core | proposto |
| RF-003 | Rappresentare plessi, classi, gruppi, docenti e studenti. | Gestione scolastica | proposto |
| RF-004 | Associare e riassegnare dispositivi secondo procedure autorizzate. | MDM | proposto |

### MDM e applicazioni

| ID | Requisito | Modulo | Stato |
|---|---|---|---|
| RF-010 | Registrare dispositivi tramite procedure di provisioning supportate. | MDM | proposto |
| RF-011 | Mantenere un inventario minimo di dispositivo e software. | MDM | proposto |
| RF-012 | Assegnare app obbligatorie e facoltative. | Application Management | proposto |
| RF-013 | Applicare configurazioni gestite e restrizioni compatibili. | MDM | proposto |
| RF-014 | Supportare profili didattici e modalità temporanee, se consentite dal provider. | Policy Engine | proposto |
| RF-015 | Registrare esito e data di sincronizzazione delle policy. | MDM | proposto |
| RF-016 | Fornire un catalogo app proprio (APK firmati) per la distribuzione senza store proprietari. | Application Management | proposto |
| RF-017 | Generare QR code di provisioning per il DPC EduWISP. | MDM | proposto |

### Family Control

| ID | Requisito | Modulo | Stato |
|---|---|---|---|
| RF-020 | Verificare l'associazione genitore/tutore-studente. | Family Control | proposto |
| RF-021 | Permettere regole familiari aggiuntive negli ambiti autorizzati. | Family Control | proposto |
| RF-022 | Rendere visibili le regole attive e la loro provenienza. | Policy Engine | proposto |
| RF-023 | Impedire che una regola familiare annulli una baseline di sicurezza. | Policy Engine | proposto |

### Cyberbullismo e benessere

| ID | Requisito | Modulo | Stato |
|---|---|---|---|
| RF-030 | Offrire un canale di segnalazione semplice e accessibile. | Cyberbullismo | proposto |
| RF-031 | Consentire segnalazioni da parte di ruoli autorizzati. | Cyberbullismo | proposto |
| RF-032 | Gestire presa in carico, assegnazione, stato e follow-up. | Cyberbullismo | proposto |
| RF-033 | Limitare l'accesso ai casi secondo necessità e ruolo. | Cyberbullismo | proposto |
| RF-034 | Conservare un audit delle consultazioni e delle modifiche. | Audit | proposto |
| RF-035 | Fornire contenuti educativi e risorse di prevenzione. | Cyberbullismo | proposto |

## Requisiti non funzionali

| ID | Requisito | Stato |
|---|---|---|
| RNF-001 | Privacy by design e minimizzazione dei dati. | proposto |
| RNF-002 | Isolamento tra tenant. | proposto |
| RNF-003 | Autenticazione robusta e autorizzazioni verificabili. | proposto |
| RNF-004 | Comunicazioni cifrate. | proposto |
| RNF-005 | Audit non alterabile dagli utenti ordinari. | proposto |
| RNF-006 | Supporto a cloud hosting e self-hosting. | proposto |
| RNF-007 | Documentazione delle API e dei limiti del provider. | proposto |
| RNF-008 | Accessibilità e usabilità per studenti e personale. | proposto |
| RNF-009 | Funzionamento resiliente con connettività intermittente, nei limiti del sistema Android. | proposto |
| RNF-010 | Procedure di backup, ripristino e gestione degli incidenti da specificare. | proposto |
| RNF-011 | Server di riferimento Debian GNU/Linux 13 (Trixie). Vedi [ADR-0004](../decisioni/0004-debian-13-server.md). | approvato |
| RNF-012 | Tutti i componenti necessari sono open source e gratuiti; nessun servizio proprietario nel core. Vedi [ADR-0009](../decisioni/0009-solo-software-libero.md). | approvato |
| RNF-013 | Protocollo server-agenti aperto, documentato e versionato. | proposto |
| RNF-014 | Core indipendente dalla piattaforma: nuove piattaforme si aggiungono con un agente e un profilo, senza modificare i moduli del core. Vedi [ADR-0011](../decisioni/0011-multipiattaforma.md). | approvato |
| RNF-015 | Ogni agente dichiara le proprie capacità; le regole non applicabili vengono mostrate, non ignorate. | approvato |
| RNF-016 | Funzionamento sui dispositivi così come venduti: nessuno sblocco del bootloader né sistema modificato; registrazione solo con metodi standard. Vedi [ADR-0003](../decisioni/0003-target-android.md). | approvato |

## Requisiti di conformità

Derivano dal [Quadro normativo](../sicurezza-privacy/quadro-normativo.md) e sono vincolanti ([ADR-0008](../decisioni/0008-conformita-normativa.md)).

| ID | Requisito | Stato |
|---|---|---|
| RC-001 | Nessun trattamento di dati reali prima di DPIA, revisione legale e parere del DPO. | approvato |
| RC-002 | Ogni dato trattato ha finalità, base giuridica e tempo di conservazione documentati. | approvato |
| RC-003 | Impostazioni predefinite sempre le più protettive (privacy by default). | approvato |
| RC-004 | Nessuna profilazione degli studenti né decisione automatizzata con effetti su di loro. | approvato |
| RC-005 | Nessuna funzione di sorveglianza occulta (messaggi, keylogging, cattura schermo, geolocalizzazione continua). | approvato |
| RC-006 | Informative e visualizzazione delle regole attive comprensibili per i minori. | approvato |
| RC-007 | Dati conservati nell'Unione europea; flussi verso terze parti mappati e documentati. | approvato |
| RC-008 | Esportazione e cancellazione dei dati per istituto e per interessato. | approvato |
| RC-009 | Strumenti per gli adempimenti della scuola: registro dei trattamenti, informative, DPIA, accordo art. 28. | proposto |
| RC-010 | Log e audit sul personale conformi all'art. 4 dello Statuto dei lavoratori. | approvato |
| RC-011 | Interfacce conformi ai requisiti di accessibilità per la PA. | proposto |
| RC-012 | Nessuna funzione di IA senza ADR dedicato, analisi AI Act e DPIA; vietato il riconoscimento delle emozioni. | approvato |

## Criteri di accettazione progettuale

Prima dello sviluppo ogni requisito dovrà avere: identificativo, motivazione, stakeholder, priorità, dipendenze, rischi, criteri verificabili e stato.
