---
title: "ADR-0013: Stack tecnologico"
parent: Decisioni (ADR)
nav_order: 13
---

# ADR-0013: Stack tecnologico

- **Stato:** Accettata
- **Data:** 2026-11-26

## Contesto

Vincoli già decisi: server di riferimento Debian 13 ([ADR-0004](0004-debian-13-server.md)), solo software libero e gratuito ([ADR-0009](0009-solo-software-libero.md)), un repository per modulo che si combinano in un'unica applicazione ([ADR-0010](0010-un-repository-per-modulo.md)), core indipendente dalla piattaforma ([ADR-0011](0011-multipiattaforma.md)), licenza AGPL-3.0-or-later ([ADR-0006](0006-licenza.md)), accessibilità per la PA e futura partecipazione a GSoC.

Versioni verificate in Debian 13 il 2026-11-26: Python 3.13, PostgreSQL 17, Valkey 8.1, Celery 5.5, nginx 1.26, Django REST Framework 3.16. Django è alla 4.2, il cui supporto ufficiale è terminato ad aprile 2026. Kotlin (1.3) e Gradle (4.4) di Debian sono troppo vecchi per lo sviluppo Android.

## Decisione

### Server

| Componente | Scelta | Licenza | Note |
|---|---|---|---|
| Linguaggio | **Python 3.13** | PSF | Da Debian 13 |
| Framework | **Django 5.2 LTS** | BSD-3-Clause | Installato con `pip` in un ambiente virtuale: supporto fino ad aprile 2028. Stesso modello di OpenWISP: ogni modulo è un'app Django installabile |
| API | **Django REST Framework**, documentazione **OpenAPI 3.1** | BSD-3-Clause | |
| Database | **PostgreSQL 17** | PostgreSQL | Da Debian 13; isolamento tra tenant verificabile |
| Attività asincrone | **Celery** con **Valkey** | BSD-3-Clause | Valkey è il fork libero di Redis, presente in Debian 13 |
| Web server | **nginx** + **gunicorn** | BSD-2-Clause / MIT | |
| Interfaccia | Template Django + **HTMX** + **Bootstrap Italia** ([Designers Italia](https://designers.italia.it/)) | BSD | Interfaccia leggera, accessibile e coerente con le linee guida di design per i servizi della PA. *Licenza di Bootstrap Italia da verificare* |
| Autenticazione | Account Django con **autenticazione a più fattori** per i ruoli privilegiati | | In futuro **SPID e CIE** per i genitori, utili alla verifica della relazione genitore-studente (RF-020): da valutare |

### Agente Android (`eduwisp-android-dpc`)

| Componente | Scelta | Note |
|---|---|---|
| Linguaggio | **Kotlin** | Apache-2.0 |
| Build | Gradle wrapper + Android Gradle Plugin | Strumenti di sviluppo, non distribuiti con EduWISP |
| Versione minima | **Android 9 (API 28)**, da confermare | Necessaria per kiosk multi-app (`setLockTaskFeatures`) e periodi di blocco degli aggiornamenti |
| Dipendenze | **Nessuna libreria Google Play Services** | Così l'agente funziona anche su dispositivi senza servizi Google |
| Notifiche dal server | Interrogazione periodica, più **[UnifiedPush](https://unifiedpush.org/)** opzionale | Firebase Cloud Messaging è proprietario ed è escluso (ADR-0009) |

### Protocollo (`eduwisp-protocol`)

- HTTPS con TLS 1.3, messaggi JSON descritti con **JSON Schema 2020-12**.
- Credenziale per dispositivo rilasciata alla registrazione (per esempio un certificato client): da definire nella specifica.

### Qualità

- Python: `pytest`, `ruff`, `pre-commit`.
- Kotlin: test JUnit, `ktlint`.
- CI con i workflow riutilizzabili dell'organizzazione.

## Alternative considerate

- **FastAPI:** moderno e veloce, ma senza amministrazione integrata e con meno supporto ai moduli riutilizzabili; si perderebbe l'esperienza di OpenWISP.
- **Java/Spring o Node.js:** validi, ma meno vicini al modello OpenWISP e alle competenze più diffuse tra studenti e comunità scolastiche.
- **Django 4.2 di Debian:** fuori dal supporto ufficiale.

## Conseguenze

- Tutte le dipendenze hanno licenze libere compatibili con l'AGPL.
- Gli strumenti per compilare l'app Android (Android SDK) sono distribuiti da Google con una propria licenza: sono strumenti di sviluppo e non fanno parte del software EduWISP. Obiettivo: build riproducibili e pubblicazione anche su F-Droid.
- Il primo prototipo usa `eduwisp-users`, `eduwisp-devices`, `eduwisp-protocol` ed `eduwisp-android-dpc`.
