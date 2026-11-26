---
title: Matrice di compatibilità Android
parent: Moduli
nav_order: 3
---

# Matrice di compatibilità Android

Questa matrice è un prerequisito per passare alla fase tecnica (vedi [Roadmap](../progetto/roadmap.md)). Ogni funzione va verificata rispetto alla modalità di gestione, al provider, alla versione Android e al produttore.

**Legenda stato:** ✅ supportata · 🟡 parziale · ❌ non supportata · 🏭 dipende da produttore/versione · ❔ da verificare

| Funzione | Fully Managed (AMAPI) | Note / fonti | Stato verifica |
|---|---|---|---|
| Provisioning tramite QR code | ❔ | | Da verificare |
| Provisioning zero-touch | ❔ | Dipende dal rivenditore | Da verificare |
| Installazione app obbligatorie | ❔ | | Da verificare |
| App facoltative (catalogo) | ❔ | | Da verificare |
| Managed configurations | ❔ | Solo app compatibili | Da verificare |
| Blocco app non consentite | ❔ | | Da verificare |
| Modalità kiosk / multi-app | ❔ | | Da verificare |
| Restrizioni impostazioni Android | ❔ | | Da verificare |
| Configurazione Wi-Fi | ❔ | | Da verificare |
| Distribuzione certificati | ❔ | | Da verificare |
| Gestione aggiornamenti di sistema | ❔ | | Da verificare |
| Blocco remoto | ❔ | | Da verificare |
| Cancellazione remota (wipe) | ❔ | | Da verificare |
| Inventario hardware/software | ❔ | | Da verificare |
| Stato e ultima sincronizzazione | ❔ | | Da verificare |
| Policy a fasce orarie | ❔ | Potrebbe richiedere logica lato server | Da verificare |
| Comportamento offline | ❔ | | Da verificare |

## Come contribuire

Per aggiornare una riga apri una issue con il modello **Verifica Android**, indicando dispositivo, versione Android, modalità di gestione, fonte ufficiale consultata ed esito del test.
