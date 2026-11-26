---
title: "ADR-0002: Modello scuola-famiglia a due ambiti coordinati"
parent: Decisioni (ADR)
nav_order: 2
---

# ADR-0002: Modello scuola-famiglia a due ambiti coordinati

- **Stato:** Accettata
- **Data:** 2026-11-26

## Contesto

Il dispositivo è di proprietà della scuola, ma viene usato anche a casa. Scuola e famiglia hanno esigenze legittime e diverse; senza regole chiare le policy entrano in conflitto in modo opaco.

## Decisione

EduWISP adotta due ambiti coordinati:

- **Ambito scolastico:** la scuola governa la gestione istituzionale, la baseline di sicurezza e le attività didattiche.
- **Ambito familiare:** il genitore/tutore può applicare regole *aggiuntive* per l'uso domestico e il tempo extrascolastico, secondo le deleghe previste.

Le regole familiari non possono annullare la baseline di sicurezza né impedire attività didattiche obbligatorie.

## Alternative considerate

- **Solo controllo scolastico:** esclude le famiglie da decisioni che riguardano il tempo extrascolastico.
- **Parità tra scuola e famiglia con sovrascrittura:** produce conflitti nascosti e può indebolire la sicurezza.

## Conseguenze

- Il [Policy Engine](../architettura/policy-engine.md) deve gestire ambiti, priorità e motivazioni esplicite.
- Serve una procedura di verifica della relazione genitore/tutore-studente (RF-020).
- Dettagli in [Family Control](../moduli/family-control.md).
