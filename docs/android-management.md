# Gestione Android

## Target

Tablet Android con Google Mobile Services, di proprietà degli istituti scolastici.

## Modalità di gestione

Fully Managed / Android Enterprise è lo scenario primario da valutare. La scelta definitiva dipende da:
- requisiti di enrollment e provisioning;
- supporto dei produttori e delle versioni Android;
- condizioni di accesso ai servizi Google;
- disponibilità e limiti delle API;
- sostenibilità per un progetto open source.

## Android Management API

L'eventuale integrazione con Android Management API deve essere preceduta da una verifica formale delle condizioni Google, dei criteri di ammissione e dei casi d'uso consentiti. Non si presume che un progetto open source ottenga automaticamente accesso o approvazione.

## Provider abstraction

Il modello dati e le policy EduWISP dovrebbero essere indipendenti dal provider. Un adapter traduce le intenzioni canoniche nelle funzionalità supportate e segnala esplicitamente quelle non disponibili.

## Matrice di compatibilità

Prima dello sviluppo occorre predisporre una matrice per ogni funzione: supportata, parzialmente supportata, non supportata, dipendente dal produttore/versione, oppure da verificare.

Funzioni da verificare: provisioning QR, Fully Managed, installazione app, managed configurations, kiosk, restrizioni, Wi-Fi, certificati, aggiornamenti, blocco, wipe, inventario e telemetria.
