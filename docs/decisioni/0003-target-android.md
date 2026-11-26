---
title: "ADR-0003: Target iniziale: tablet Android GMS school-owned, Fully Managed"
parent: Decisioni (ADR)
nav_order: 3
---

# ADR-0003: Target iniziale: tablet Android GMS school-owned, Fully Managed

- **Stato:** Proposta
- **Data:** 2026-11-26

## Contesto

Serve un perimetro iniziale ristretto per poter verificare concretamente le funzionalità di gestione.

## Decisione proposta

- Dispositivi: tablet Android con Google Mobile Services, di proprietà della scuola.
- Modalità di gestione primaria: **Android Enterprise Fully Managed**.
- Il BYOD è fuori dal perimetro iniziale.
- Il core resta indipendente dal provider tramite un *provider adapter*.

## Punti da verificare prima dell'accettazione

- Condizioni di accesso ad Android Management API per un progetto open source.
- Compilazione della [matrice di compatibilità](../moduli/android-matrice-compatibilita.md).
- Supporto dei produttori e delle versioni Android diffusi nelle scuole.

## Conseguenze

Se AMAPI non fosse utilizzabile, andranno valutati provider alternativi senza cambiare il modello dati di EduWISP.
