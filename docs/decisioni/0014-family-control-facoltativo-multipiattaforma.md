---
title: "ADR-0014: Family Control facoltativo e multipiattaforma"
parent: Decisioni (ADR)
nav_order: 14
---

# ADR-0014: Family Control facoltativo e multipiattaforma

- **Stato:** Accettata (principi). Gli aspetti tecnici per Apple e la titolarità dei dati sono aperti.
- **Data:** 2026-11-27

## Contesto

Le famiglie usano servizi commerciali di parental control (per esempio Qustodio) per gestire il tempo e i contenuti sui dispositivi dei figli. Sono proprietari, a pagamento e trattano i dati dei minori presso fornitori esterni. EduWISP può offrire un'alternativa **open source e gratuita**, integrata con le regole della scuola ([ADR-0002](0002-modello-scuola-famiglia.md)).

## Decisione

1. **Facoltativo, scelto dal genitore.** Il Family Control si attiva **solo** su richiesta del genitore o tutore, che può disattivarlo in ogni momento. La scuola non può attivarlo, imporlo o condizionarlo. EduWISP funziona completamente anche senza.
2. **Dispositivi coperti:**
   - il **tablet della scuola**, con regole aggiuntive per l'uso a casa (ADR-0002);
   - i **dispositivi della famiglia**: telefoni e tablet Android, **PC Windows e Linux** nella prima fase; **Apple (macOS, iPhone, iPad) in programma** per una fase successiva (vedi i vincoli sotto).
3. **Dati separati dalla scuola.** I dati del Family Control stanno in un dominio separato. La scuola **non vede nulla** dei dispositivi della famiglia. Sul tablet della scuola vede solo che esistono regole familiari attive (per gestire i conflitti), non i dati d'uso.
4. **Funzioni ammesse:**
   - limiti di tempo giornalieri e **fasce orarie** (per esempio niente dispositivo dopo le 21);
   - **filtro dei contenuti web** per categorie e liste, con liste aperte;
   - app consentite e bloccate, per app o per categoria;
   - **riepiloghi d'uso aggregati** (tempo per app e per giorno), visibili **anche al figlio**;
   - richiesta di **tempo extra** da parte del figlio, approvata dal genitore;
   - pausa immediata del dispositivo.
5. **Funzioni escluse:** lettura di messaggi, chat ed email; keylogging; screenshot o registrazione dello schermo; registrazione delle chiamate; **geolocalizzazione continua** (RC-005). La localizzazione su richiesta, con avviso visibile al figlio, è da valutare con un ADR dedicato.
6. **Trasparenza verso il figlio:** l'agente è sempre visibile e mai nascosto; il figlio può vedere quali regole sono attive e quali dati vengono raccolti, in linguaggio adatto all'età. Le impostazioni predefinite si adattano all'età (**autonomia progressiva**).
7. **Agenti dedicati** (ADR-0010, ADR-0011), che usano lo stesso protocollo aperto:
   - `eduwisp-desktop-agent`: un solo codice per Windows, macOS e Linux;
   - `eduwisp-family-android`: app Android per i dispositivi personali, senza modalità *device owner* e quindi **senza ripristino di fabbrica**;
   - il server `eduwisp-family`.
8. **Solo software libero** ([ADR-0009](0009-solo-software-libero.md)): filtri, liste e agenti open source; nessun servizio cloud proprietario.

## Vincoli e punti aperti

| Tema | Vincolo | Stato |
|---|---|---|
| **iPhone e iPad** | Le API di parental control di Apple richiedono l'autorizzazione *Family Controls* concessa da Apple, e la distribuzione passa dall'App Store e dall'**Apple Developer Program, a pagamento**. | **In programma** (fase successiva) |
| **macOS** | Senza notarizzazione Apple (Developer ID, a pagamento) macOS blocca o avvisa all'installazione. Senza le API Apple le funzioni possibili sono più limitate. | **In programma** (fase successiva) |
| **Windows** | Senza firma digitale Windows SmartScreen mostra avvisi. **SignPath Foundation** offre firma gratuita ai progetti open source con build automatica. | Da richiedere |
| **Android personale** | Senza *device owner* servono permessi standard (statistiche d'uso, VPN locale per il filtro, accessibilità). Le regole di Google Play su questi permessi sono severe: distribuzione anche tramite F-Droid o catalogo proprio. | Da verificare |
| **Linux** | Nessun vincolo di distribuzione; servizio di sistema con filtro DNS. | — |
| **Titolare dei dati** | Chi gestisce il server del Family Control: la scuola (in un dominio separato), un fornitore scelto dalla famiglia o la famiglia stessa in self-hosting. Cambia chi è titolare e chi responsabile del trattamento. | Da decidere con un legale |
| **Genitori separati** | Entrambi possono esercitare la responsabilità genitoriale: va definito come gestire regole e consensi. | Da valutare con un legale |
| **Figli dai 14 anni** | Età del consenso digitale in Italia: valutare informazione e coinvolgimento diretto del ragazzo. | Da valutare |

## Conseguenze

- Il perimetro si allarga ai **dispositivi della famiglia**, ma solo tramite il Family Control facoltativo: la scuola continua a gestire solo i propri dispositivi (il BYOD scolastico resta fuori perimetro).
- Il protocollo e il modello delle policy devono gestire anche fasce orarie, limiti di tempo e filtri web, in modo indipendente dalla piattaforma.
- Servono una DPIA dedicata e una revisione legale prima di trattare dati reali (ADR-0008).
