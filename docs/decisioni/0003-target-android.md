---
title: "ADR-0003: Target Android e strada tecnica di gestione"
parent: Decisioni (ADR)
nav_order: 3
---

# ADR-0003: Target Android e strada tecnica di gestione

- **Stato:** Proposta
- **Data:** 2026-11-26 (rivista dopo la verifica della matrice e l'ADR-0009)

## Contesto

Serve un perimetro iniziale ristretto. La [matrice di compatibilità](../moduli/android-matrice-compatibilita.md) mostra due strade: Android Management API (proprietaria, riservata a EMM commerciali) e un DPC proprio basato sulle API Android (open source). L'[ADR-0009](0009-solo-software-libero.md) impone componenti open source e gratuiti.

## Decisione proposta

- **Dispositivi:** tablet Android di proprietà della scuola, gestiti in modalità **Fully Managed** (*device owner*). Il BYOD è fuori perimetro.
- **Dispositivi così come venduti:** EduWISP deve funzionare sui dispositivi con il sistema originale del produttore. Sono esclusi lo sblocco del bootloader e l'installazione di sistemi modificati: una scuola non li farebbe mai. La registrazione avviene solo con i metodi standard (ripristino di fabbrica + QR code).
- **Agente:** un **DPC EduWISP open source** che usa direttamente `DevicePolicyManager` e comunica con il server EduWISP tramite un protocollo aperto e documentato.
- **App:** un **catalogo app EduWISP** (repository di APK firmati, sul modello di F-Droid) gestito dal server della scuola o del fornitore.
- **Provisioning:** QR code con download del DPC dal server EduWISP. Lo zero-touch è da verificare.
- **Android Management API:** esclusa dal core (ADR-0009).
- Il modello dati resta indipendente dal provider tramite il *provider adapter*.

## Rischio bloccante aperto: approvazione del DPC sui dispositivi Google

Dal 2025, sui dispositivi con servizi Google, Play Protect blocca durante la registrazione i DPC non verificati da Android Enterprise. Possibili risposte, da valutare:

1. **Chiedere la verifica** del DPC EduWISP ad Android Enterprise. **È la strada principale**, perché i tablet acquistati dalle scuole hanno quasi sempre i servizi Google. Il DPC resta open source; l'approvazione è un controllo di sicurezza esterno, non una dipendenza dal software di Google. Il processo per nuovi DPC non è documentato pubblicamente.
2. **Dispositivi venduti senza servizi Google** dal produttore: nessun blocco Play Protect, ma l'offerta per le scuole è molto limitata. Resta un'opzione marginale. Lo sblocco o la modifica del sistema sono esclusi.

*Da verificare:* se il blocco riguarda tutti i metodi di provisioning, incluso il QR con URL di download, e da quale versione Android.

## Punti aperti

- Le app proprietarie usate dalle scuole e distribuite solo su Google Play: va definito se e come renderle disponibili senza managed Google Play, senza associare account Google personali ai minori.
- Test su 2-3 modelli di tablet diffusi nelle scuole.

## Conseguenze

Il progetto si fa carico dello sviluppo e della manutenzione dell'agente Android e del catalogo app. In cambio ottiene il controllo completo, il funzionamento offline delle fasce orarie e nessun trasferimento di dati di gestione verso terzi.
