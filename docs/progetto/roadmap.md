---
title: Roadmap
parent: Progetto
nav_order: 2
---

# Roadmap

La roadmap è progettuale e non indica date o promesse di rilascio.

| Fase | Attività | Stato |
|---|---|---|
| 1 | Visione e perimetro | In definizione |
| 2 | Requisiti funzionali e non funzionali | Da validare |
| 3 | Modello scuola-famiglia | Concordato ([ADR-0002](../decisioni/0002-modello-scuola-famiglia.md)) |
| 4 | Requisiti Cyberbullying & Digital Wellbeing | Da approfondire |
| 5 | Architettura logica e domini | Proposta |
| 6 | Verifica formale delle possibilità Android | Documentazione verificata, test su dispositivi da fare ([matrice](../moduli/android-matrice-compatibilita.md)) |
| 7 | Sicurezza, privacy e valutazione DPIA | Da approfondire |
| 8 | Governance e scelta licenza | Decise ([ADR-0006](../decisioni/0006-licenza.md), [ADR-0012](../decisioni/0012-responsabile-del-progetto.md)) |
| 9 | Specifiche tecniche | Non iniziata |
| 10 | Sviluppo | Non iniziato |

## Ambienti

- **Ora:** `demo.eduwisp.org` su `server.eduwisp.org`, solo con dati fittizi.
- **Dopo i requisiti legali:** `pilota.eduwisp.org` con scuole aderenti ([ADR-0015](../decisioni/0015-ambienti-del-progetto.md)).

## Installazione del server: ordine dei lavori

1. **Architettura del server**: decisa in [ADR-0016](../decisioni/0016-architettura-del-server.md) e nella pagina [Architettura del server](../architettura/server.md).
2. **Ruolo `ansible-eduwisp`** completato di conseguenza (oggi: applicazione, database, web, firewall, IDS, hardening).
3. **ISO di installazione**, per ultima. Requisiti già raccolti:
   - installatore **guidato in stile Proxmox**: disco, rete e indirizzo IP, nome del server, email dell'amministratore, password;
   - **logo EduWISP** nel menu di avvio (BIOS e UEFI) e nell'installatore;
   - basata sull'installatore ufficiale di **Debian stable**, verificato con firma GPG;
   - **aggiornata automaticamente**: una GitHub Action controlla ogni giorno se esce una nuova versione di Debian stable e ricostruisce e pubblica la ISO;
   - al primo avvio una procedura guidata configura EduWISP con il ruolo Ansible.

## In programma per le fasi successive

- **Family Control su dispositivi Apple** (macOS, iPhone, iPad): richiede l'autorizzazione *Family Controls* di Apple e l'Apple Developer Program ([ADR-0014](../decisioni/0014-family-control-facoltativo-multipiattaforma.md)).

## Obiettivo: Google Summer of Code

Il progetto punta a candidarsi come organizzazione mentore di [Google Summer of Code](https://summerofcode.withgoogle.com/). Requisiti (edizione 2026): software rilasciato con licenza OSI, almeno 18 mesi di storia, una comunità con mentori disponibili, una politica sull'uso dell'IA. Obiettivo realistico: **GSoC 2029**, oppure prima tramite un'organizzazione ombrello.

## Criteri per passare alla fase tecnica

- Requisiti prioritari approvati.
- Matrice di compatibilità Android verificata.
- Modello dei ruoli e delle responsabilità approvato.
- Analisi privacy e sicurezza completata a livello progettuale.
- Quadro normativo validato da DPO e consulenti legali; DPIA preliminare redatta.
- Licenza e governance definite.
- Architettura tecnica motivata e documentata.
