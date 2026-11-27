---
title: Informativa dell'app EduWISP Scuola
parent: Sicurezza e privacy
nav_order: 5
---

# Informativa privacy dell'app «EduWISP Scuola»

*Ultimo aggiornamento: 27 novembre 2026.* 🇬🇧 [English](/docs/en/security-privacy/app-school/)

L'app **EduWISP Scuola** (`org.eduwisp.scuola`) è un software libero (licenza AGPL-3.0-or-later) del progetto EduWISP per il personale delle scuole: docenti, coordinatori e dirigenti. Codice sorgente: <https://github.com/EduWISP/eduwisp-app-scuola>.

## Chi tratta i dati

L'app si collega **al server EduWISP del tuo istituto**, che indichi al primo accesso. I dati che vedi (classi, studenti, tablet, richieste di app) sono trattati dall'**istituto scolastico**, che ne è titolare: per l'informativa completa e per esercitare i tuoi diritti rivolgiti all'istituto. Il progetto EduWISP non riceve questi dati.

L'ambiente di prova `demo.eduwisp.org` contiene **solo dati inventati**.

## Quali dati usa l'app

| Dato | Dove | Perché |
|---|---|---|
| Indirizzo del server dell'istituto | sul telefono | per collegarsi |
| Nome utente e password | inviati solo al server dell'istituto, via HTTPS, al momento dell'accesso; **la password non viene salvata** | per accedere |
| Token di accesso | sul telefono, **cifrato** con il Keystore di Android; sul server solo la sua impronta | per restare collegati (30 giorni, revocabile) |
| Nome del modello del telefono | inviato al server dell'istituto | per riconoscere il telefono nell'elenco degli accessi |
| Ruolo scelto, numero di richieste in attesa | sul telefono | per il menu e per le notifiche |

L'app **non salva dati degli studenti** sul telefono: li chiede al server ogni volta. Le notifiche indicano solo **quante** richieste di app sono in attesa, senza nomi.

## Cosa l'app non fa

- Non usa la posizione, la fotocamera, il microfono, i contatti o i file del telefono.
- Non contiene pubblicità, statistiche, tracciamento o servizi di terzi (niente Firebase né Google Play Services).
- Non condivide dati con nessuno oltre al server dell'istituto.
- Non fa backup nel cloud né trasferimenti ad altri dispositivi.

## Sicurezza e conservazione

Tutte le comunicazioni usano HTTPS. Uscendo dall'app il token viene **revocato** sul server; disinstallando l'app i dati sul telefono vengono cancellati. Sul server, la conservazione segue le regole dell'istituto ([quadro normativo](quadro-normativo.md)).

## Contatti

Progetto EduWISP: <https://eduwisp.org> · [gruppo di discussione](https://groups.google.com/g/eduwisp-sviluppo). Per i dati trattati dalla scuola: il tuo istituto e il suo responsabile della protezione dei dati.
