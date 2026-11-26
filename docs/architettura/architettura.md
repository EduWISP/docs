---
title: Architettura concettuale
parent: Architettura
nav_order: 1
---

# Architettura concettuale

## Principi

- Separazione dei domini funzionali.
- Core indipendente dal provider MDM.
- Solo componenti open source e gratuiti, nessun servizio cloud proprietario nel core ([ADR-0009](../decisioni/0009-solo-software-libero.md)).
- API documentate e versionate.
- Multi-tenancy e isolamento dei dati.
- Audit e autorizzazioni trasversali.
- Evoluzione modulare senza imporre microservizi prematuri.

## Domini logici

1. **Core & Identity:** tenant, utenti, ruoli, gruppi e autorizzazioni.
2. **School Management:** istituti, plessi, classi, docenti e studenti.
3. **Device Management:** inventario, lifecycle e assegnazioni.
4. **Provider Adapter:** traduzione tra modello canonico e provider Android.
5. **Application Management:** catalogo e assegnazioni delle applicazioni.
6. **Policy Engine:** composizione e valutazione delle regole.
7. **Family Control:** deleghe e policy familiari.
8. **Cyberbullying & Wellbeing:** segnalazioni e gestione dei casi.
9. **Audit & Reporting:** eventi amministrativi e report minimizzati.
10. **Presentation & API:** portali e integrazioni.

## Schema concettuale

```text
School Portal     Family Portal     Student Reporting
      |                 |                    |
      +-----------------+--------------------+
                        |
                 Identity & Core
                        |
       +----------------+-------------------+
       |                |                   |
 School Management  Family Control   Case Management
       |                |                   |
       +----------------+-------------------+
                        |
                   Policy Engine
                        |
                Device Management
                        |
                 Provider Adapter
                        |
         Protocollo aperto server ↔ agente
                        |
        DPC EduWISP (device owner) + catalogo app
```

## Ipotesi tecnologiche

Framework, database, codebase e modalità di esecuzione non sono ancora decisioni. La scelta dovrà considerare competenze della comunità, manutenibilità, sicurezza, accessibilità, costi e supporto a Debian 13.

## Multi-tenancy

La progettazione dovrà definire confini tenant, isolamento delle query, gestione degli amministratori di piattaforma, esportazione e cancellazione dei dati, audit e procedure di backup. L'isolamento deve essere verificabile e testabile.
