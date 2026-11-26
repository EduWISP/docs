---
title: "ADR-0011: Architettura indipendente dalla piattaforma dei dispositivi"
parent: Decisioni (ADR)
nav_order: 11
---

# ADR-0011: Architettura indipendente dalla piattaforma dei dispositivi

- **Stato:** Accettata
- **Data:** 2026-11-26

## Contesto

Il primo obiettivo sono i tablet Android, ma in futuro le scuole potrebbero voler gestire anche altri sistemi (per esempio computer GNU/Linux, Windows, ChromeOS o altri dispositivi). Se il core venisse progettato attorno ad Android, aggiungere una piattaforma richiederebbe di riscriverlo.

## Decisione

1. **Il core di EduWISP non conosce Android.** Gestione scolastica, Policy Engine, Family Control, catalogo app e audit lavorano su un **modello canonico** di dispositivo, policy e applicazione.
2. Ogni piattaforma si integra con un **agente** dedicato in un proprio repository (`eduwisp-<piattaforma>-agent` o equivalente, oggi `eduwisp-android-dpc`), che parla con il server tramite `eduwisp-protocol`.
3. `eduwisp-protocol` è **multipiattaforma**: messaggi comuni a tutti gli agenti, più **profili di piattaforma** per le funzioni specifiche.
4. Ogni agente **dichiara le proprie capacità** (per esempio kiosk, fasce orarie offline, wipe). Il Policy Engine mostra esplicitamente quali regole non sono applicabili su un dato dispositivo, invece di ignorarle in silenzio.
5. Il catalogo app gestisce **tipi di pacchetto diversi** per piattaforma (oggi APK).
6. Ogni nuova piattaforma ha la propria **matrice di compatibilità** e deve rispettare ADR-0008 (conformità) e ADR-0009 (solo software libero e gratuito).

## Conseguenze

- Il modello canonico va progettato con attenzione, evitando concetti esclusivi di Android nel core.
- Le funzioni non comuni a tutte le piattaforme vivono nei profili di piattaforma e negli agenti.
- Aggiungere una piattaforma significa scrivere un agente e un profilo, senza modificare i moduli del core.
