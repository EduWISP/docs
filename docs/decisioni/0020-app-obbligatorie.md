---
title: "ADR-0020: App obbligatorie installate automaticamente"
parent: Decisioni (ADR)
nav_order: 20
---

# ADR-0020: App obbligatorie installate automaticamente

- **Stato:** Accettata
- **Data:** 2026-11-27

## Contesto

Con l'[ADR-0019](0019-app-consentite.md) le app obbligatorie sono segnalate allo studente con un pulsante «Installa». L'istituto vuole invece che si **installino da sole**, senza chiedere nulla allo studente, e vuole gestire le app da **un unico elenco** di app consentite, con una spunta per quelle obbligatorie e il **logo** di ciascuna.

Android installa app in silenzio solo in due modi:

1. il proprietario del dispositivo (il DPC EduWISP) installa un **file APK** che ha scaricato;
2. **Google Play gestito** (Android Enterprise) installa le app del Play Store su richiesta dell'MDM.

Scaricare gli APK dal Play Store per ridistribuirli non è consentito. Le app proprietarie (per esempio Teams, MyLIM, didUP di Argo) si possono quindi installare in silenzio solo con un APK fornito dall'editore o con Google Play gestito. Google Play gestito però richiede un account Google per ogni istituto, lega la piattaforma a un servizio proprietario e, secondo l'istituto, ha costi: non è compatibile con l'[ADR-0009](0009-solo-software-libero.md).

## Decisione

1. **Elenco unico**: nel catalogo dell'istituto ogni app consentita ha una spunta **«obbligatoria»** (per tutti, per un indirizzo o per una classe) e può avere il suo **logo**, mostrato nel portale e sul tablet.
2. **Installazione silenziosa da APK** (subito, software libero): l'istituto può caricare nel catalogo l'APK di un'app (un'app libera, oppure un APK fornito dall'editore). Per le app obbligatorie con APK, il tablet lo scarica dal server della scuola con la propria credenziale, ne **verifica l'impronta SHA-256** e lo installa **senza chiedere nulla**. Gli APK non sono pubblici: li scaricano solo i dispositivi dell'istituto.
3. Un'app obbligatoria **senza APK** resta segnalata allo studente con il pulsante «Installa» dell'ADR-0019, che apre lo store sul tablet.
4. **Le app vietate non diventano mai obbligatorie** e un APK di un'app vietata viene rifiutato.

## Alternative considerate

- **Google Play gestito** (Android Enterprise): installerebbe in silenzio qualsiasi app del Play Store, ma richiede un account Google aziendale per ogni istituto, dipende da un servizio proprietario e ha costi. Scartata (ADR-0009).
- **Solo il pulsante «Installa»**: nessuna installazione automatica. Scartata: l'istituto vuole che le app obbligatorie si installino da sole quando possibile.

## Conseguenze

- `eduwisp-apps`: spunta «obbligatoria» nelle app consentite (sostituisce l'elenco separato), logo e APK nel catalogo, download degli APK solo per i dispositivi autenticati dell'istituto.
- Protocollo v0: per le app obbligatorie, nella policy, l'indirizzo e l'impronta dell'APK (campo facoltativo `install`).
- DPC: download, verifica dell'impronta e installazione silenziosa con `PackageInstaller`.
- Server: spazio per gli APK, non servito pubblicamente da nginx e incluso nei backup.
- Da fare: app consentite **per il singolo studente** (per esempio gli strumenti del PDP per gli studenti con DSA, che il Garante chiede di consentire, FAQ 12), senza registrare il motivo e visibili solo a chi segue lo studente ([quadro normativo](../sicurezza-privacy/quadro-normativo.md#indicazioni-del-garante-per-le-scuole)).
- L'installazione avviene già al primo ciclo dopo la registrazione del tablet; se non riesce, si ritenta a ogni sincronizzazione (al più ogni 10 minuti per la stessa app).
