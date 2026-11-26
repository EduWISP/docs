---
title: "ADR-0010: Un repository per ogni modulo"
parent: Decisioni (ADR)
nav_order: 10
---

# ADR-0010: Un repository per ogni modulo

- **Stato:** Accettata
- **Data:** 2026-11-26

## Contesto

EduWISP vuole crescere come progetto comunitario. Chi contribuisce deve poter **prendere in carico un modulo in modo indipendente**: svilupparlo, testarlo, rilasciarlo e mantenerlo senza dover conoscere tutto il resto. [OpenWISP](https://github.com/openwisp), a cui il progetto si ispira, adotta con successo questo modello.

## Decisione

1. **Ogni modulo ha un proprio repository** nell'organizzazione `EduWISP`, con il proprio responsabile (*module owner*), le proprie issue, la propria CI e le proprie versioni.
2. Ogni modulo è **installabile e testabile da solo**, dipendendo solo dai moduli di base (`eduwisp-users`, `eduwisp-utils`) e dalle interfacce documentate degli altri moduli.
3. **Repository separati non significa microservizi:** come in OpenWISP, i moduli server si combinano in un'unica applicazione installabile (vedi [Architettura](../architettura/architettura.md)).
4. Agente Android, specifica del protocollo, strumenti di installazione e documentazione hanno ciascuno un repository dedicato.
5. Ogni repository rispetta la struttura minima comune descritta in [Organizzazione dei repository](../architettura/repository.md).
6. I repository dei moduli sono stati creati il 2026-11-26, in stato di progettazione, per permettere a chi vuole di prendere in carico un modulo fin da subito. La progettazione di dettaglio resta in `EduWISP/docs` finché il modulo non entra in sviluppo.

## Alternative considerate

- **Monorepo:** più semplice da coordinare, ma rende difficile affidare un modulo a un gruppo indipendente e mescola cicli di rilascio diversi.

## Conseguenze

- Servono interfacce tra moduli stabili e documentate, e regole chiare sulle dipendenze.
- Serve una CI condivisa (workflow riutilizzabili) per non duplicare la configurazione in ogni repository.
- Serve un processo di **rilascio coordinato** della piattaforma, con una combinazione di versioni dei moduli testata insieme.
- La documentazione di ciascun modulo vive nel suo repository e viene raccolta nel sito unico.
