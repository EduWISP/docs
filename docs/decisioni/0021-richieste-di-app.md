---
title: "ADR-0021: Richieste di app e app per il singolo studente"
parent: Decisioni (ADR)
nav_order: 21
---

# ADR-0021: Richieste di app e app per il singolo studente

- **Stato:** Accettata
- **Data:** 2026-11-27

## Contesto

Con l'elenco di app consentite ([ADR-0019](0019-app-consentite.md)) un'app non prevista viene sospesa. Lo studente deve poter chiedere di usarla, la famiglia deve poter dire la sua, la decisione spetta ai docenti e deve restare traccia per il coordinatore e il dirigente. Inoltre il Garante chiede che gli studenti con DSA possano usare gli strumenti previsti dal PDP (FAQ «Scuola e privacy» n. 12): servono app consentite per **un singolo studente**, senza registrare il motivo ([quadro normativo](../sicurezza-privacy/quadro-normativo.md#indicazioni-del-garante-per-le-scuole)).

## Decisione

1. **App per il singolo studente**: una regola delle app consentite può valere per un solo studente (oltre che per istituto, indirizzo o classe). Non si registra il motivo. La vedono solo il dirigente, i docenti della classe, la famiglia dello studente e gli amministratori.
2. **Richiesta dal tablet**: sul proprio tablet lo studente vede le app sospese e può premere **«Chiedi alla scuola»**, con una breve motivazione facoltativa. Parte solo la richiesta per quell'app: nessun elenco delle app installate arriva al server. Si chiede solo dai tablet personali, non da quelli condivisi.
3. **Parere della famiglia**: i familiari collegati possono dare un **parere favorevole con una motivazione** (obbligatoria). Per gli studenti maggiorenni solo se lo studente ha consentito l'accesso ai familiari ([ADR-0018](0018-interfaccia-per-ruoli.md)).
4. **Decisione del docente**: decide **un docente della classe** dello studente, approvando o respingendo con una **motivazione obbligatoria**. Se approva, l'app diventa consentita **solo per quello studente**.
5. **Visibilità e registrazione**: la richiesta, i pareri e la decisione restano registrati. Li vedono i docenti della classe (compreso il coordinatore), il dirigente e la famiglia; mai in elenchi o bacheche generali (FAQ 6 e 7). Ogni decisione va anche nel registro delle operazioni.
6. **App vietate** (social, VPN, Tor…): la richiesta viene respinta subito, con la spiegazione; nessuno la può approvare.
7. **Notifiche**: nel portale, docenti della classe, coordinatore, dirigente e famiglia vedono le richieste in attesa. Le email arriveranno con il modulo delle notifiche.

## Alternative considerate

- **Notificare ogni app bloccata**: richiederebbe di inviare al server quali app ci sono sul tablet, contro la minimizzazione. Scartata: si notifica solo ciò che lo studente chiede.
- **Decisione del solo coordinatore** o del dirigente: più lenta. Scartata; il coordinatore e il dirigente vedono comunque tutto.

## Conseguenze

- Protocollo v0: nuovo messaggio `app-request` (`POST /api/protocol/v0/app-requests`).
- `eduwisp-apps`: regole per studente, richieste, pareri e decisioni; `eduwisp-audit`: eventi delle decisioni.
- `eduwisp-portal`: pagine delle richieste per docenti, dirigente e famiglia.
- DPC: elenco delle app sospese con «Chiedi alla scuola».
