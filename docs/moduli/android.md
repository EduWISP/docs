---
title: Gestione Android
parent: Moduli
nav_order: 2
---

# Gestione Android

## Target

Tablet Android di proprietà degli istituti scolastici, gestiti in modalità **Fully Managed** (*device owner*), con o senza servizi Google (GMS). Proposta in [ADR-0003](../decisioni/0003-target-android.md).

## Strada tecnica

Per l'[ADR-0009](../decisioni/0009-solo-software-libero.md) ogni componente deve essere open source e gratuito. La gestione avviene quindi con componenti sviluppati dal progetto:

| Componente | Ruolo |
|---|---|
| **DPC EduWISP** | App open source installata come *device owner*: applica policy, restrizioni, kiosk, aggiornamenti e fasce orarie, anche offline |
| **Protocollo server-agente** | Interfaccia aperta, documentata e versionata tra il server EduWISP e il DPC |
| **Catalogo app EduWISP** | Repository di APK firmati (sul modello di F-Droid) da cui il DPC installa e aggiorna le app in modo silenzioso |
| **Provisioning** | QR code generato dal server EduWISP, che scarica e installa il DPC al primo avvio |

## Android Management API

**Esclusa dal core.** È un servizio proprietario Google riservato a EMM commerciali, OEM e fornitori di Device Trust, con quote soggette ad approvazione e trattamento dei dati da parte di Google. Resta nella matrice solo come termine di confronto.

## Rischio aperto: dispositivi con servizi Google

Sui dispositivi con GMS, Play Protect consente durante la registrazione solo i DPC approvati da Android Enterprise. La strada principale è **far verificare il DPC EduWISP** da Android Enterprise; i dispositivi devono restare così come venduti, senza sblocchi né sistemi modificati (ADR-0003, RNF-016).

## Provider abstraction

Il modello dati e le policy EduWISP restano indipendenti dall'agente. Un adapter traduce le intenzioni canoniche nelle funzionalità supportate dal dispositivo e segnala esplicitamente quelle non disponibili.

## Matrice di compatibilità

Lo stato di ogni funzione è nella [matrice di compatibilità](android-matrice-compatibilita.md).
