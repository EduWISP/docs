---
title: Family Control
parent: Moduli
nav_order: 5
---

# Family Control

Un parental control **open source e gratuito**, integrato con le regole della scuola. È **facoltativo**: lo attiva solo il genitore o tutore ([ADR-0014](../decisioni/0014-family-control-facoltativo-multipiattaforma.md)).

## Due ambiti coordinati

Decisione registrata in [ADR-0002](../decisioni/0002-modello-scuola-famiglia.md).

- **Ambito scolastico:** la scuola governa la gestione istituzionale, le baseline di sicurezza e le attività didattiche sul tablet della scuola.
- **Ambito familiare:** il genitore/tutore può aggiungere regole per l'uso domestico e il tempo extrascolastico.

Le regole familiari non possono annullare la sicurezza né impedire la didattica obbligatoria.

## Dispositivi

| Dispositivo | Come | Stato |
|---|---|---|
| Tablet della scuola | Regole familiari aggiuntive applicate dal DPC EduWISP | Previsto |
| Telefoni e tablet Android della famiglia | App `eduwisp-family-android`, **senza ripristino di fabbrica** | Previsto |
| PC Windows | `eduwisp-desktop-agent` | Previsto (firma: SignPath Foundation da richiedere) |
| PC macOS | `eduwisp-desktop-agent` | Da verificare (notarizzazione Apple a pagamento) |
| PC Linux | `eduwisp-desktop-agent` | Previsto |
| iPhone e iPad | — | Da valutare (autorizzazione Apple e programma sviluppatori a pagamento) |

## Funzioni

**Previste:** limiti di tempo giornalieri, fasce orarie, filtro dei contenuti web per categorie, app consentite e bloccate, riepiloghi d'uso aggregati visibili anche al figlio, richiesta di tempo extra, pausa immediata.

**Escluse:** lettura di messaggi, chat ed email; keylogging; screenshot o registrazione dello schermo; registrazione delle chiamate; geolocalizzazione continua.

## Principi

- **Scelta del genitore:** attivazione esplicita, disattivazione in ogni momento; la scuola non può imporlo.
- **Dati separati:** la scuola non vede nulla dei dispositivi della famiglia; sul tablet della scuola vede solo l'esistenza di regole familiari, non i dati d'uso.
- **Trasparenza verso il figlio:** agente visibile, regole e dati consultabili in linguaggio adatto all'età, impostazioni predefinite che crescono con l'età.
- **Nessuna copia di servizi esistenti:** EduWISP non usa nomi, marchi o interfacce di prodotti commerciali.

## Verifica della relazione

La relazione genitore/tutore-studente va verificata con una procedura definita dall'istituto (in futuro anche con SPID o CIE). Vanno gestiti deleghe, affidamento, variazioni e revoche senza esporre informazioni familiari non necessarie. Per i dispositivi solo familiari la verifica scolastica non è necessaria.

## Conflitti

Le regole non si risolvono con una semplice sovrascrittura. Ogni policy dichiara ambito, priorità, periodo, origine e motivazione. I conflitti sul tablet della scuola vengono mostrati e risolti secondo criteri documentati ([Policy Engine](../architettura/policy-engine.md)).

## Punti aperti

Titolarità dei dati, genitori separati, coinvolgimento dei figli dai 14 anni, supporto Apple: vedi [ADR-0014](../decisioni/0014-family-control-facoltativo-multipiattaforma.md).
