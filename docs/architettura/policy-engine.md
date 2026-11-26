---
title: Policy Engine
parent: Architettura
nav_order: 2
---

# Policy Engine

## Scopo

Definire, combinare e rendere comprensibili le regole che governano il dispositivo nei diversi contesti.

## Dimensioni di una policy

- soggetto e dispositivo destinatario;
- tenant, istituto, plesso, classe o gruppo;
- ambito (sicurezza, didattica, famiglia);
- periodo e calendario;
- origine e responsabile;
- priorità e motivazione;
- funzionalità richieste e compatibilità provider.

## Principi di composizione

La baseline di sicurezza non può essere indebolita da policy meno privilegiate. Le policy scolastiche obbligatorie per l'attività didattica devono essere riconoscibili. Le policy familiari possono aggiungere limiti nel proprio ambito, ma non annullare sicurezza e didattica obbligatoria.

## Risultato effettivo

Il sistema dovrebbe mostrare:
- regola applicata;
- fonte della regola;
- motivazione;
- eventuale conflitto;
- compatibilità con il dispositivo/provider;
- stato di distribuzione e ultima sincronizzazione.

## Offline

Le policy già distribuite possono restare attive in assenza di rete, se il provider lo consente. La progettazione deve definire scadenza, orologio attendibile, comportamento fail-safe e gestione delle policy non aggiornate.
