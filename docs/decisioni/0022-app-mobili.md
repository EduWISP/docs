---
title: "ADR-0022: App mobili per personale, studenti e famiglie"
parent: Decisioni (ADR)
nav_order: 22
---

# ADR-0022: App mobili per personale, studenti e famiglie

- **Stato:** Accettata
- **Data:** 2026-11-27

## Contesto

Il portale web ([ADR-0018](0018-interfaccia-per-ruoli.md)) funziona da qualsiasi browser, ma docenti, dirigenti e famiglie usano soprattutto il telefono, spesso personale. Il progetto ha un account sviluppatore Google Play e due gruppi Google: [eduwisp-sviluppo](https://groups.google.com/g/eduwisp-sviluppo) per le discussioni ed [eduwisp-tester](https://groups.google.com/g/eduwisp-tester) per i test chiusi.

## Decisione

1. **Tre app**, ciascuna nel proprio repository ([ADR-0010](0010-un-repository-per-modulo.md)):
   - `eduwisp-app-scuola` per il personale: **menu diverso** per docente, coordinatore e dirigente;
   - `eduwisp-app-famiglia` per i genitori e i tutori; in seguito con il **controllo familiare completo** del modulo Family Control ([ADR-0014](0014-family-control-facoltativo-multipiattaforma.md)), con dati separati da quelli della scuola;
   - `eduwisp-app-studente` per gli studenti.
2. **Prima Android**, con app **native in Kotlin** pubblicate su Google Play; iOS in una fase successiva.
3. **Un'API JSON per le app** (nuovo modulo `eduwisp-api`, `/api/app/v1/`) che usa **gli stessi permessi del portale**: il docente vede solo le proprie classi, il dirigente l'istituto, la famiglia solo i propri figli. Il menu dell'app viene dal server, secondo il ruolo.
4. **Accesso**: utente e password dell'istituto; il server rilascia un **token** per quel telefono, conservato cifrato nel Keystore di Android, con scadenza e revocabile; in seguito l'autenticazione a più fattori. L'account pubblico `demo`/`demo` della demo funziona anche nelle app, **in sola lettura**: serve anche alla revisione di Google Play.
5. **Nessun servizio proprietario nelle app** ([ADR-0009](0009-solo-software-libero.md)): niente Firebase né Google Play Services. Le novità (per esempio le richieste di app da decidere) arrivano con un controllo periodico del server; in seguito con UnifiedPush, che è libero.
6. **Minimizzazione**: le app mostrano gli stessi dati del portale e non salvano copie permanenti sul telefono oltre a quanto serve per la sessione; niente dati sanitari, niente posizione.
7. **Test chiuso** su Google Play con il gruppo eduwisp-tester prima della pubblicazione.

## Conseguenze

- Nuovo modulo `eduwisp-api` (dipende da users, school, devices, apps, audit).
- Nuovo repository `eduwisp-app-scuola`; poi le app per famiglie e studenti.
- Ansible: limite di richieste sull'accesso dell'API come per `/accedi/`.
