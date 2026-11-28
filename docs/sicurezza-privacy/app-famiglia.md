---
title: Informativa dell'app EduWISP Famiglia
parent: Sicurezza e privacy
nav_order: 6
---

# Informativa privacy dell'app «EduWISP Famiglia»

*Ultimo aggiornamento: 28 novembre 2026.* 🇬🇧 [English](/docs/en/security-privacy/app-family/)

L'app **EduWISP Famiglia** (`org.eduwisp.famiglia`) è un software libero (licenza AGPL-3.0-or-later) del progetto EduWISP per genitori e tutori degli studenti. Codice sorgente: <https://github.com/EduWISP/eduwisp-app-famiglia>.

## Chi tratta i dati

L'app si collega **al server EduWISP della scuola**, che indichi al primo accesso. I dati che vedi sui tuoi figli (classe, tablet della scuola, app consentite, richieste di app) sono trattati dall'**istituto scolastico**, che ne è titolare: per l'informativa completa e per esercitare i tuoi diritti rivolgiti all'istituto. Il progetto EduWISP non riceve questi dati.

L'ambiente di prova `demo.eduwisp.org` contiene **solo dati inventati**.

## Cosa vedi

- **Solo i tuoi figli**, con gli stessi permessi del portale web della scuola.
- Dalla **maggiore età** vedi i dati di tuo figlio solo se lo consente dal suo tablet; altrimenti vedi soltanto che è maggiorenne ([ADR-0018](../decisioni/0018-interfaccia-per-ruoli.md)).

## Quali dati usa l'app

| Dato | Dove | Perché |
|---|---|---|
| Indirizzo del server della scuola | sul telefono | per collegarsi |
| Nome utente e password | inviati solo al server della scuola, via HTTPS, al momento dell'accesso; **la password non viene salvata** | per accedere |
| Token di accesso | sul telefono, **cifrato** con il Keystore di Android; sul server solo la sua impronta | per restare collegati (30 giorni, revocabile) |
| Nome del modello del telefono | inviato al server della scuola | per riconoscere il telefono nell'elenco degli accessi |
| Parere sulle richieste di app, con la motivazione | inviato al server della scuola | per il parere della famiglia: resta registrato ed è visibile a docenti, coordinatore e dirigente ([ADR-0021](../decisioni/0021-richieste-di-app.md)) |
| Ruolo scelto, numero di richieste che aspettano un parere | sul telefono | per il menu e per le notifiche |

L'app **non salva dati dei figli** sul telefono: li chiede al server ogni volta. Le notifiche indicano solo **quante** richieste aspettano il tuo parere, senza nomi.

## Cosa l'app non fa

- Non usa la posizione, la fotocamera, il microfono, i contatti o i file del telefono.
- Non contiene pubblicità, statistiche, tracciamento o servizi di terzi (niente Firebase né Google Play Services).
- Non condivide dati con nessuno oltre al server della scuola.
- Non fa backup nel cloud né trasferimenti ad altri dispositivi.
- Non controlla il telefono dei figli: il controllo familiare sui dispositivi della famiglia sarà un modulo facoltativo e separato ([ADR-0014](../decisioni/0014-family-control-facoltativo-multipiattaforma.md)).

## Sicurezza e conservazione

Tutte le comunicazioni usano HTTPS. Uscendo dall'app il token viene **revocato** sul server; disinstallando l'app i dati sul telefono vengono cancellati. Sul server, la conservazione segue le regole dell'istituto ([quadro normativo](quadro-normativo.md)).

## Cancellazione dei dati

L'app **EduWISP Famiglia** non crea account: l'account lo crea e lo gestisce la **scuola**.

1. **Dati sul telefono**: premi **Esci** nell'app (il token viene revocato anche sul server) oppure disinstalla l'app. Indirizzo del server, token e preferenze vengono cancellati subito.
2. **Dati sul server della scuola** (account, elenco degli accessi, pareri sulle richieste di app): chiedi la cancellazione alla scuola, cioè alla segreteria o al responsabile della protezione dei dati (art. 17 GDPR).
3. La scuola cancella l'account e gli accessi. I pareri sulle richieste di app restano conservati per il tempo previsto dalle sue regole sui registri scolastici, poi vengono cancellati.

Il progetto EduWISP non conserva dati degli utenti dell'app e non può cancellarli al posto della scuola.

## Contatti

Progetto EduWISP: <https://eduwisp.org> · [gruppo di discussione](https://groups.google.com/g/eduwisp-sviluppo). Per i dati trattati dalla scuola: la scuola e il suo responsabile della protezione dei dati.
