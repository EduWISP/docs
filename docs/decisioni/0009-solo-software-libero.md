---
title: "ADR-0009: Solo componenti open source e gratuiti"
parent: Decisioni (ADR)
nav_order: 9
---

# ADR-0009: Solo componenti open source e gratuiti

- **Stato:** Accettata
- **Data:** 2026-11-26

## Contesto

La verifica della [matrice di compatibilità Android](../moduli/android-matrice-compatibilita.md) ha mostrato che Android Management API, Android Device Policy e managed Google Play sono servizi **proprietari** di Google. L'accesso è riservato a soggetti commerciali e soggetto a quote e approvazione.

## Decisione

1. Ogni componente necessario al funzionamento di EduWISP (server, agente sul dispositivo, catalogo app, strumenti di provisioning) deve essere **open source e gratuito**.
2. Se una funzione richiede un servizio proprietario, **il progetto ne sviluppa un'alternativa libera**, oppure la funzione resta fuori dal perimetro.
3. Le dipendenze di terze parti devono avere licenze libere compatibili con quella del progetto (vedi [ADR-0006](0006-licenza.md)).
4. Non si integrano nel core servizi cloud proprietari, nemmeno se gratuiti.

## Conseguenze

- Android Management API e managed Google Play **escono dal core** del progetto.
- La strada tecnica primaria diventa un **DPC EduWISP open source** in modalità *device owner*, con un **catalogo app proprio** (vedi [ADR-0003](0003-target-android.md)).
- Il progetto deve sviluppare e mantenere l'agente Android, con il relativo costo di manutenzione al cambiare delle versioni Android.
- Coerenza con la privacy: i dati di gestione restano sui server EduWISP, nell'UE o in self-hosting, senza trasferimenti verso servizi di gestione di terzi.
- Resta un **vincolo esterno** che non dipende dal codice: sui dispositivi con servizi Google, Play Protect consente la registrazione solo di DPC approvati da Android Enterprise (vedi ADR-0003).
