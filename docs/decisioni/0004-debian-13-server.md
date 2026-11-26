---
title: "ADR-0004: Debian GNU/Linux 13 come piattaforma server di riferimento"
parent: Decisioni (ADR)
nav_order: 4
---

# ADR-0004: Debian GNU/Linux 13 come piattaforma server di riferimento

- **Stato:** Accettata
- **Data:** 2026-11-26

## Contesto

Le scuole e i fornitori che fanno self-hosting hanno bisogno di una piattaforma server stabile, libera e con supporto di lungo periodo.

## Decisione

Debian GNU/Linux 13 (Trixie) è il sistema operativo di riferimento per il server EduWISP.

## Conseguenze

- Runtime, database e dipendenze devono essere disponibili e mantenibili su Debian 13.
- Il requisito riguarda la piattaforma server: non implica che ogni container debba usare Debian come immagine base.
- Le scelte di runtime, database e packaging restano da prendere (vedi [Deployment](../architettura/deployment.md)).
