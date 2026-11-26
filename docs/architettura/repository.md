---
title: Organizzazione dei repository
parent: Architettura
nav_order: 4
---

# Organizzazione dei repository

Ogni modulo ha un proprio repository, così che qualcuno possa prenderlo in carico in modo indipendente ([ADR-0010](../decisioni/0010-un-repository-per-modulo.md)). Il modello è ispirato a [OpenWISP](https://github.com/openwisp).

{: .note }
> I nomi sono una proposta. I repository verranno creati quando ciascun modulo entrerà in sviluppo.

## Mappa dei repository

### Moduli di base

| Repository | Contenuto | Equivalente OpenWISP |
|---|---|---|
| `eduwisp-utils` | Utility condivise, controlli di qualità, componenti comuni dell'interfaccia | `openwisp-utils` |
| `eduwisp-users` | Core & Identity: tenant, utenti, ruoli, autorizzazioni, multi-tenancy | `openwisp-users` |
| `eduwisp-audit` | Registro delle operazioni e report minimizzati | — |

### Moduli funzionali (server)

| Repository | Contenuto | Documentazione |
|---|---|---|
| `eduwisp-school` | Istituti, plessi, classi, docenti, studenti, assegnazioni | [Gestione scolastica](../moduli/gestione-scolastica.md) |
| `eduwisp-devices` | MDM: inventario, ciclo di vita, comandi, provisioning | [MDM](../moduli/mdm.md) |
| `eduwisp-policy` | Policy Engine: composizione, conflitti, policy effettiva | [Policy Engine](policy-engine.md) |
| `eduwisp-apps` | Catalogo app (APK firmati), assegnazioni, configurazioni gestite | [Gestione Android](../moduli/android.md) |
| `eduwisp-family` | Family Control: deleghe e regole familiari | [Family Control](../moduli/family-control.md) |
| `eduwisp-wellbeing` | Segnalazioni e gestione dei casi di cyberbullismo, benessere digitale | [Cyberbullismo](../moduli/cyberbullismo.md) |

### Dispositivo e protocollo

| Repository | Contenuto | Equivalente OpenWISP |
|---|---|---|
| `eduwisp-protocol` | Specifica aperta e versionata del protocollo server-agenti, multipiattaforma: messaggi comuni, profili di piattaforma, capacità degli agenti, test di conformità | `netjsonconfig` / NetJSON |
| `eduwisp-android-dpc` | DPC EduWISP open source (*device owner*), primo agente | `openwisp-config` (agente OpenWrt) |
| `eduwisp-desktop-agent` | Agente per PC Windows, macOS e Linux, per il Family Control (da creare, [ADR-0014](../decisioni/0014-family-control-facoltativo-multipiattaforma.md)) | — |
| `eduwisp-family-android` | App Family Control per dispositivi Android personali, senza *device owner* (da creare) | — |
| `eduwisp-<piattaforma>-agent` | Agenti per altre piattaforme, in futuro ([ADR-0011](../decisioni/0011-multipiattaforma.md)) | `openwrt-openwisp-monitoring` |

### Installazione

| Repository | Contenuto | Equivalente OpenWISP |
|---|---|---|
| `ansible-eduwisp` | Installazione e aggiornamento su Debian 13 | `ansible-openwisp2` |
| `docker-eduwisp` | Immagini e composizione container | `docker-openwisp` |

### Progetto

| Repository | Contenuto |
|---|---|
| `.github` | Profilo, file comuni della comunità, modelli di issue e PR, workflow riutilizzabili |
| `docs` | Progettazione, ADR e sito che raccoglie la documentazione di tutti i moduli |

## Dipendenze

| Modulo | Dipende da |
|---|---|
| `eduwisp-utils` | — |
| `eduwisp-users` | utils |
| `eduwisp-audit` | utils, users |
| `eduwisp-school` | utils, users, audit |
| `eduwisp-devices` | utils, users, audit, school, protocol |
| `eduwisp-apps` | utils, users, audit, devices |
| `eduwisp-policy` | utils, users, audit, school, devices, apps |
| `eduwisp-family` | utils, users, audit, school, policy |
| `eduwisp-wellbeing` | utils, users, audit, school |
| `eduwisp-protocol` | — (specifica indipendente) |
| `eduwisp-android-dpc` | protocol |

Regole:

- Le dipendenze vanno **in una sola direzione**, verso i moduli di base. Niente cicli.
- Un modulo usa un altro modulo **solo tramite interfacce documentate** (API, eventi, punti di estensione), mai accedendo ai suoi dati interni.
- Il server e gli agenti dipendono entrambi da `eduwisp-protocol`, e nessuno dei due dall'altro: così si può sostituire un lato o aggiungere una piattaforma senza toccare il core.
- `eduwisp-wellbeing` tratta i dati più delicati: dominio separato, accesso ristretto, nessuna dipendenza in ingresso dagli altri moduli funzionali.

## Struttura minima di ogni repository

Presa da OpenWISP e adattata:

| File o cartella | Scopo |
|---|---|
| `README.md` | Cosa fa il modulo, stato, come provarlo (italiano, con riepilogo in inglese) |
| `docs/user/`, `docs/developer/` | Documentazione d'uso e per sviluppatori, raccolta nel sito unico |
| `CHANGES.md` | Registro delle modifiche per versione |
| `LICENSE` | Licenza scelta con [ADR-0006](../decisioni/0006-licenza.md) |
| `CODEOWNERS` | Responsabile del modulo e revisori |
| `publiccode.yml` | Metadati per il catalogo [Developers Italia](https://developers.italia.it/) del riuso nella PA |
| `tests/` | Test automatici, inclusi quelli di isolamento tra tenant |
| `.github/workflows/` | CI tramite i workflow riutilizzabili dell'organizzazione |
| `PRIVACY.md` | Dati personali trattati dal modulo, finalità, conservazione e riferimenti al [quadro normativo](../sicurezza-privacy/quadro-normativo.md) |

`CONTRIBUTING`, codice di condotta, `SECURITY` e modelli di issue vengono ereditati dal repository `.github`.

## Versioni e rilasci

- Ogni modulo ha un **versionamento semantico** proprio.
- Periodicamente si pubblica un **rilascio della piattaforma** con una combinazione di versioni dei moduli testata insieme, come fanno le versioni della documentazione di OpenWISP.

## Responsabili dei moduli

Chi vuole prendere in carico un modulo lo propone in [Discussions](https://github.com/EduWISP/docs/discussions). Il *module owner* viene indicato in `CODEOWNERS` e nella [governance](../progetto/governance.md).
