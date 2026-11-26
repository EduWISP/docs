---
title: "ADR-0006: Licenze del codice, della documentazione e del marchio"
parent: Decisioni (ADR)
nav_order: 6
---

# ADR-0006: Licenze del codice, della documentazione e del marchio

- **Stato:** Accettata
- **Data:** 2026-11-26
- **Deciso da:** responsabile del progetto ([ADR-0012](0012-responsabile-del-progetto.md))

## Contesto

Requisiti espressi dal responsabile del progetto:

1. EduWISP deve essere **open source**, con licenza approvata dall'OSI, anche per poter partecipare in futuro a **Google Summer of Code**.
2. Le **scuole pubbliche** devono poterlo usare e riusare secondo il CAD (art. 68-69) e le Linee guida AgID.
3. Chi lo usa deve **sempre citare EduWISP**.
4. Nessuno deve poterne fare **un proprio prodotto chiuso** o spacciarsi per EduWISP.

Le [Linee guida AgID su acquisizione e riuso del software](https://docs.italia.it/italia/developers-italia/lg-acquisizione-e-riuso-software-per-pa-docs/it/stabile/riuso-software/licenze-aperte-e-scelta-di-una-licenza.html) (par. 3.5) chiedono una licenza certificata OSI e indicano: EUPL-1.2 per il software nuovo in generale, **AGPL-3.0-or-later per il software usato principalmente via rete** (per esempio da browser), BSD-3-Clause per le librerie, CC BY 4.0 per la documentazione tecnica.

## Decisione

| Cosa | Licenza |
|---|---|
| **Codice** (moduli server, agenti, protocollo, strumenti di installazione) | **AGPL-3.0-or-later** con termini aggiuntivi ai sensi della sezione 7 |
| **Documentazione e testi** | **CC BY-SA 4.0** |
| **Nome e logo EduWISP** | Esclusi dalle licenze aperte; regolati dalla [politica del marchio](../progetto/marchio.md) |
| **Contributi** | **DCO** (*Developer Certificate of Origin*), con `git commit -s`; il copyright resta ai contributori |

Termini aggiuntivi AGPL (file `NOTICE.md` in ogni repository di codice):

- **7(b) attribuzione:** conservare le note di copyright e mostrare nelle note legali dell'interfaccia la dicitura «Basato su EduWISP — https://github.com/EduWISP».
- **7(c) origine:** vietato presentare in modo ingannevole l'origine; le versioni modificate devono essere indicate come diverse dall'originale.
- **7(e) marchi:** nessun diritto su nome e logo; le versioni modificate distribuite devono usare un nome diverso, salvo autorizzazione.

Copyright: «Michele Salerno e i contributori di EduWISP».

## Perché non altre licenze

- **EUPL-1.2:** ottima per la PA e ufficiale in italiano, ma la sua clausola di compatibilità permette di ridistribuire i derivati con altre licenze, anche senza obbligo per l'uso via rete, e l'attribuzione nell'interfaccia è meno incisiva. AgID stessa indica l'AGPL per il software usato via rete.
- **Licenze permissive** (MIT, BSD, Apache): consentirebbero versioni chiuse.
- **Licenze che vietano i fork o l'uso commerciale:** non sono open source, quindi violerebbero l'[ADR-0009](0009-solo-software-libero.md) ed escluderebbero EduWISP dal riuso nella PA e da GSoC.

## Limiti da conoscere

- Come in ogni progetto open source, **un fork resta sempre possibile**. Deve però restare AGPL, citare EduWISP e usare un altro nome.
- La tutela del nome tramite licenza è contrattuale. Una tutela piena richiede la **registrazione del marchio** (UIBM o EUIPO), da valutare.
- Una scelta di licenza non è consulenza legale: testo dei termini aggiuntivi e politica del marchio vanno fatti verificare da un legale.

## Conseguenze

- Ogni repository di codice contiene `LICENSE`, `NOTICE.md`, `publiccode.yml` (per il catalogo Developers Italia) e il controllo DCO.
- Le interfacce di EduWISP dovranno avere una pagina «Informazioni» con l'attribuzione e il link al codice sorgente, come richiesto dall'AGPL (sezione 13).
