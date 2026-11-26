---
title: "ADR-0005: Modello di distribuzione cloud-first ma self-hostable"
parent: Decisioni (ADR)
nav_order: 5
---

# ADR-0005: Modello di distribuzione cloud-first ma self-hostable

- **Stato:** Accettata
- **Data:** 2026-11-26

## Contesto

Molte scuole preferiscono un servizio gestito; altre, o reti di istituti, vogliono mantenere il controllo dell'infrastruttura e dei dati.

## Decisione

EduWISP è progettato **cloud-first** (esperienza di gestione e priorità progettuale) ma deve essere sempre **installabile autonomamente**. Il core non dipende obbligatoriamente da un servizio cloud proprietario.

## Conseguenze

- L'architettura deve restare portabile e documentata.
- La documentazione dovrà coprire dimensionamento, aggiornamenti, backup e ripristino per il self-hosting.
