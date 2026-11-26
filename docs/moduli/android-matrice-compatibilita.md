---
title: Matrice di compatibilità Android
parent: Moduli
nav_order: 3
---

# Matrice di compatibilità Android

Questa matrice è un prerequisito per passare alla fase tecnica (vedi [Roadmap](../progetto/roadmap.md)). Confronta le due strade tecniche possibili per gestire tablet **Fully Managed** di proprietà della scuola:

- **AMAPI**: Android Management API, servizio cloud Google, con l'app Google *Android Device Policy* sul dispositivo.
- **DPC EduWISP**: un'app di gestione open source del progetto, installata come *device owner*, che usa direttamente le API Android (`DevicePolicyManager`).

**Legenda:** ✅ documentata · 🟡 parziale o con limiti · ❌ non disponibile · ❔ non confermata dalla documentazione · ⚠️ vincolo bloccante

{: .important }
> **Stato della verifica:** documentazione ufficiale consultata il **2026-11-26**. Nessuna funzione è stata ancora **provata su dispositivi reali**: «documentata» non significa «funziona sui tablet delle scuole». I livelli API marcati «da confermare» non sono stati verificati sulle singole pagine di riferimento.

## 1. Condizioni di accesso (vincolo bloccante)

| Aspetto | AMAPI | DPC EduWISP |
|---|---|---|
| Chi può usarla | ⚠️ Riservata a «sviluppatori EMM commerciali, fornitori di soluzioni Device Trust e OEM», con un **contratto diretto con i clienti finali** | Le API sono parte di Android (AOSP) e chiunque può usarle |
| Quote | ⚠️ Quota iniziale **fino a 500 dispositivi** con giustificazione aziendale completa; oltre, richiesta ad Android Enterprise. Al massimo **2 progetti per sviluppatore** | Nessuna quota Google |
| Approvazione Google | Implicita nell'accesso alla quota | ⚠️ Dal 2025 solo i DPC **verificati e approvati** da Android Enterprise possono essere installati durante la registrazione: gli altri vengono bloccati da Play Protect («App blocked to protect your device»). Il processo di approvazione per nuovi DPC non è documentato pubblicamente |
| Costo | Nessun costo indicato nelle condizioni d'uso | Gratuite |
| Managed Google Play | ✅ Incluso | ❌ Le nuove registrazioni di DPC personalizzati alla Google Play EMM API sono chiuse: le app si possono distribuire solo come APK propri |
| Usi vietati da Google | Monitoraggio o intercettazione di dispositivi e utenti; finanziamento con blocco; installazione di app senza «consenso espresso e informato» | Stessi criteri, applicati alla verifica Play Protect |
| Flussi di dati | ⚠️ Dati del dispositivo trattati da Google: la localizzazione non è indicata nelle pagine lette. Va valutata come trasferimento GDPR e nella DPIA | I dati restano sui server EduWISP (UE, self-hosting possibile) |
| Modello self-hosted | 🟡 Ogni installazione autonoma avrebbe bisogno di un proprio progetto Google con quota approvata | ✅ Compatibile |

## 2. Funzioni

| Funzione | AMAPI | DPC EduWISP | Note |
|---|---|---|---|
| Provisioning con QR code | ✅ Android 7.0+ | ⚠️ Supportato dalle API (`EXTRA_PROVISIONING_DEVICE_ADMIN_PACKAGE_DOWNLOAD_LOCATION`), ma **bloccato se il DPC non è approvato** | Da Android 12 il DPC deve gestire `ACTION_GET_PROVISIONING_MODE` e `ACTION_ADMIN_POLICY_COMPLIANCE` |
| Provisioning zero-touch | ✅ Android 8.0+ (Pixel 7.1+), dispositivi da **rivenditore zero-touch autorizzato** | ❔ | Utile per acquisti in blocco delle scuole |
| App obbligatorie | ✅ `installType`: `FORCE_INSTALLED`, `REQUIRED_FOR_SETUP` | ✅ Installazione silenziosa del *device owner* con `PackageInstaller` | DPC: solo APK propri, non app del Play Store |
| App facoltative (catalogo) | ✅ `AVAILABLE` tramite managed Google Play | 🟡 Solo da un catalogo APK proprio | |
| Blocco delle app non consentite | ✅ `playStoreMode` in lista consentita (le altre app vengono disinstallate), `BLOCKED` | ✅ `setApplicationHidden`, `setPackagesSuspended`, `setUninstallBlocked` | Livelli API DPC da confermare |
| Managed configurations | ✅ `managedConfiguration` | ✅ `setApplicationRestrictions` | Solo per app che le supportano |
| Kiosk mono-app | 🟡 `installType: KIOSK` (deprecato) | ✅ Lock task, Android 5.0+ | |
| Kiosk multi-app (modalità verifica) | ✅ `kioskCustomLauncherEnabled`, `kioskCustomization` | ✅ `setLockTaskPackages`; `setLockTaskFeatures` da Android 9 | |
| Restrizioni | ✅ `cameraAccess`, `microphoneAccess`, `screenCaptureDisabled`, `factoryResetDisabled`, `usbDataAccess`, `advancedSecurityOverrides.developerSettings`, `addUserDisabled`, `bluetoothDisabled`, … | ✅ `addUserRestriction` con `DISALLOW_FACTORY_RESET`, `DISALLOW_SAFE_BOOT`, `DISALLOW_DEBUGGING_FEATURES`, `DISALLOW_USB_FILE_TRANSFER`, …; `setCameraDisabled`, `setScreenCaptureDisabled` | |
| Configurazione Wi-Fi | ✅ `openNetworkConfiguration` (ONC) | ❔ | DPC: verificare i limiti di `WifiManager` da Android 10 |
| Certificati | 🟡 CA tramite ONC (implicito); certificati client non chiariti | ✅ `installCaCert`, `installKeyPair` | Necessari per reti Wi-Fi 802.1X delle scuole |
| Aggiornamenti di sistema | ✅ `systemUpdate`: `AUTOMATIC`, `WINDOWED`, `POSTPONE` (30 giorni); `freezePeriods` (max 90 giorni, a 60 giorni di distanza) | ✅ `SystemUpdatePolicy` (Android 6.0+), periodi di blocco da Android 9 | Utile per bloccare gli aggiornamenti durante gli esami |
| Blocco remoto | ✅ Comando `LOCK`, modalità smarrimento `START_LOST_MODE` | ✅ `lockNow` | |
| Riavvio remoto | ✅ `REBOOT` (Android 7.0+) | ❔ | |
| Cancellazione remota | ✅ Comando `WIPE` con `wipeParams` (ripristino di fabbrica) | ✅ `wipeData` / `wipeDevice` | Azione ad alto impatto: doppia conferma e audit (vedi [MDM](mdm.md)) |
| Pulizia dati di un'app | ✅ `CLEAR_APP_DATA` (Android 9+) | ❔ | Utile per la riassegnazione dei tablet |
| Inventario hardware/software | ✅ `hardwareInfo`, `softwareInfo`, `applicationReports`, `memoryInfo`, `networkInfo`, ciascuno attivabile con `statusReportingSettings` | ✅ Raccolta dall'app; numero di serie accessibile al *device owner* | **Minimizzazione:** attivare solo i dati necessari. `networkInfo` include IMEI e MAC |
| Stato e ultima sincronizzazione | ✅ `lastPolicySyncTime`, `lastStatusReportTime`, `policyCompliant`, `nonComplianceDetails` | ✅ Da implementare nel protocollo EduWISP | |
| Policy a fasce orarie (scuola/casa) | 🟡 Nessuna pianificazione nativa: va cambiata la policy dal server, e serve connessione | ✅ Logica locale nell'app, funziona anche offline | Fondamentale per il [Family Control](family-control.md) |
| Limiti di tempo per singola app | ❌ Non trovato | 🟡 Possibile con `setPackagesSuspended` e statistiche d'uso | DPC: accesso alle statistiche d'uso da confermare |
| Comportamento offline | 🟡 Nessuna dichiarazione esplicita; dopo **270 giorni** offline il dispositivo va riprovisionato | 🟡 Dipende dall'implementazione; serve un orologio attendibile | |

## 3. Cosa ne consegue

Con l'[ADR-0009](../decisioni/0009-solo-software-libero.md) (solo componenti open source e gratuiti) **la colonna AMAPI resta solo come termine di confronto**: Android Management API, Android Device Policy e managed Google Play sono proprietari ed escono dal core.

La strada primaria è il **DPC EduWISP** ([ADR-0003](../decisioni/0003-target-android.md)). Dalla matrice emergono le alternative che il progetto deve costruire:

| Funzione proprietaria da sostituire | Alternativa libera EduWISP |
|---|---|
| Android Device Policy (agente Google) | **DPC EduWISP** open source, *device owner* |
| Android Management API (cloud Google) | **Server EduWISP** con protocollo aperto e documentato tra server e agente |
| Managed Google Play | **Catalogo app EduWISP**: repository di APK firmati, sul modello di F-Droid |
| Zero-touch (portale Google) | Provisioning con **QR code** generato dal server EduWISP; zero-touch da verificare |

Punti da risolvere:

1. ⚠️ **Approvazione del DPC sui dispositivi con servizi Google.** Play Protect blocca i DPC non verificati. Le opzioni sono in ADR-0003: chiedere la verifica, usare dispositivi AOSP, oppure un approccio misto.
2. **App disponibili solo su Google Play.** Va definito se e come offrirle senza managed Google Play e senza account Google personali dei minori.
3. **Righe ❔ della colonna DPC** (Wi-Fi, zero-touch, riavvio, pulizia dati app): da verificare.
4. **Test su dispositivi reali** di 2-3 modelli diffusi nelle scuole.

## Fonti

Consultate il 2026-11-26.

- [Android Management API — permissible usage](https://developers.google.com/android/management/permissible-usage)
- [AMAPI — Provision a device](https://developers.google.com/android/management/provision-device)
- [AMAPI — enterprises.policies](https://developers.google.com/android/management/reference/rest/v1/enterprises.policies)
- [AMAPI — enterprises.devices](https://developers.google.com/android/management/reference/rest/v1/enterprises.devices)
- [AMAPI — issueCommand](https://developers.google.com/android/management/reference/rest/v1/enterprises.devices/issueCommand)
- [Approved Android Enterprise DPC allowlist](https://support.google.com/work/android/answer/16694822)
- [Build a device policy controller](https://developer.android.com/work/dpc/build-dpc)
- [DevicePolicyManager](https://developer.android.com/reference/android/app/admin/DevicePolicyManager)
- [Lock task mode](https://developer.android.com/work/dpc/dedicated-devices/lock-task-mode)
- [SystemUpdatePolicy](https://developer.android.com/reference/android/app/admin/SystemUpdatePolicy)
- [PackageInstaller](https://developer.android.com/reference/android/content/pm/PackageInstaller)
- Fonte secondaria, non ufficiale: J. Bayton, [The DPC allowlist](https://bayton.org/blog/2025/12/the-dpc-allowlist/) (dicembre 2025) e [AMAPI vs custom DPC](https://bayton.org/android/android-enterprise-faq/amapi-vs-custom-dpc/)

## Come contribuire

Per aggiornare una riga apri una issue con il modello **Verifica Android**, indicando dispositivo, versione Android, strada tecnica, fonte ufficiale ed esito del test.
