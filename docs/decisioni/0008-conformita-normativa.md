---
title: "ADR-0008: Conformità normativa come vincolo bloccante"
parent: Decisioni (ADR)
nav_order: 8
---

# ADR-0008: Conformità normativa come vincolo bloccante

- **Stato:** Accettata
- **Data:** 2026-11-26

## Contesto

EduWISP gestisce dispositivi usati da **minori**, in scuole che sono in gran parte pubbliche amministrazioni. Gli errori di progettazione possono danneggiare persone vulnerabili e esporre gli istituti a responsabilità.

## Decisione

1. Il rispetto della normativa italiana ed europea (GDPR, Codice privacy, norme su minori e cyberbullismo, AI Act, Statuto dei lavoratori, norme sulla PA) è un **vincolo bloccante**: una funzionalità non conforme non viene progettata né sviluppata, indipendentemente dalla sua utilità.
2. Il [quadro normativo](../sicurezza-privacy/quadro-normativo.md) è mantenuto come documento vivo e ogni modulo deve indicare le norme che lo riguardano.
3. Nessun dato reale viene trattato prima di DPIA, revisione legale e coinvolgimento del DPO.
4. Nel dubbio si sceglie l'opzione **più protettiva per il minore**.

## Conseguenze

- Le proposte di funzionalità devono includere una valutazione privacy (modello di issue *Privacy e sicurezza*).
- La revisione legale e privacy è un criterio di uscita della fase di progettazione (vedi [Roadmap](../progetto/roadmap.md)).
- Il progetto cercherà il contributo di DPO, giuristi ed esperti di tutela dei minori.
