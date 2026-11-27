---
title: "ADR-0019: App consentite"
parent: Decisioni (ADR)
nav_order: 19
---

# ADR-0019: App consentite

- **Stato:** Accettata
- **Data:** 2026-11-27

## Contesto

I tablet della scuola sono usati da minori. La scuola deve decidere quali app si possono usare, in modo semplice per chi amministra e trasparente per chi usa il tablet. Il catalogo di APK firmati previsto da RF-016 richiede più lavoro, e alcune app vanno vietate in ogni caso per la tutela dei minori (social, VPN, Tor); nel frattempo serve un controllo sulle app già presenti e su quelle che arrivano da uno store.

## Decisione

1. **Elenco di app consentite** (*allowlist*): sul tablet si usano solo le app consentite. Le altre app con un'icona vengono **sospese**: restano visibili in grigio e, se si aprono, Android mostra che sono bloccate dalla scuola. Una app installata dopo, per esempio dal Play Store se la scuola lo consente, viene sospesa al controllo successivo (al massimo 15 minuti). Se il Play Store non è consentito, è sospeso anch'esso: non si installa nulla, ma si fermano anche gli aggiornamenti automatici delle app; per questo è consigliato consentirlo oppure usare il catalogo di APK firmati quando sarà pronto.
2. **Livelli** (si sommano):
   - **istituto**: base valida per tutti i tablet;
   - **indirizzo** e **classe**: app aggiuntive;
   - **sblocco temporaneo del docente**: durante la lezione un docente può sbloccare un'app del catalogo dell'istituto per **una delle sue classi**, per una durata limitata (al massimo 4 ore). Lo sblocco ha una scadenza scritta nella policy: il tablet richiude l'app da solo anche senza rete. Ogni sblocco è registrato.
3. **Cataloghi**:
   - **catalogo della piattaforma**, deciso solo dall'amministratore di sistema: app **consentite in tutti gli istituti** (istruzione, ufficio e comunicazione, per esempio Google Classroom, Microsoft Teams, MyLIM, Booktab, didUP di Argo, GeoGebra, WhatsApp) e app **vietate ovunque**;
   - **catalogo dell'istituto**: le altre app che la scuola conosce (nome e identificativo del pacchetto). Solo le app dei cataloghi si possono consentire o sbloccare.
4. **App vietate** (categorie social, incontri, VPN, Tor, browser con VPN integrata): sempre sospese, anche negli istituti che non usano l'elenco di app consentite (modalità `blocklist`); nessun istituto né docente le può consentire o sbloccare.
5. **App obbligatorie**, scelte da ogni istituto (per tutti, per indirizzo o per classe), tra quelle consentite: il tablet le mostra allo studente con il nome e il collegamento allo store finché non sono installate, e la scuola vede che mancano.
6. **VPN e DNS privato**: per impostazione predefinita non si possono configurare (`vpn_config_disabled`, `private_dns_config_disabled`), così nessuna app VPN può attivarsi e non si aggirano i filtri.
7. **App protette**: il tablet non sospende mai il DPC EduWISP, la schermata Home, le tastiere attive e i componenti di sistema senza icona, per non rendere il dispositivo inutilizzabile. L'agente le segnala se compaiono tra quelle da bloccare.
8. **Installazioni da fonti sconosciute vietate** in entrambe le modalità.
9. **Protocollo v0**: la policy contiene `apps` con la modalità, gli identificativi consentiti (con eventuale scadenza, obbligatorietà e nome) e quelli vietati. Gli identificativi dipendono dalla piattaforma (per Android il nome del pacchetto). L'agente dichiara la capacità `apps:allowlist`.
10. **Nessun inventario delle app installate** inviato al server nella v0: la scuola non vede quali app ci sono sul tablet, solo se la policy è applicata (minimizzazione).

## Alternative considerate

- **Elenco di app bloccate** (*blocklist*): tutto è permesso tranne le app indicate. Più semplice, ma ogni nuova app è subito disponibile: non adatto a dispositivi per minori.
- **App nascoste invece che sospese**: più pulito, ma lo studente non capisce perché un'app sparisce. Scartata per trasparenza.
- **Managed Google Play**: richiede servizi proprietari di Google (ADR-0009). Rinviato; resta il catalogo di APK firmati (RF-016).

## Conseguenze

- `eduwisp-apps` riceve il primo codice: catalogo, regole per istituto, indirizzo e classe, sblocchi temporanei.
- `eduwisp-devices` compone la policy con i contributi di altri moduli (impostazione `EDUWISP_POLICY_PROVIDERS`), così non dipende da `eduwisp-apps`.
- `eduwisp-portal`: nella pagina della classe il docente sblocca e richiude le app.
- DPC: sospensione delle app a ogni sincronizzazione e richiusura alla scadenza degli sblocchi anche offline.
