# EduWISP — Documentazione

🇮🇹 Documentazione di progetto di **EduWISP**, piattaforma open source per la gestione dei dispositivi Android di proprietà delle scuole.
🇬🇧 *Design documentation for **EduWISP**, an open-source platform for managing school-owned Android devices. English version: <https://eduwisp.github.io/docs/en/>.*

📖 **Sito:** <https://eduwisp.github.io/docs/>

> **Stato: progettazione.** Questo repository contiene solo documentazione e specifiche concettuali: nessun server MDM, nessuna app Android, nessuna procedura di installazione.

## Struttura

```
docs/                      sorgente del sito (Jekyll + just-the-docs)
├── index.md               home (italiano)
├── progetto/              visione, roadmap, governance, glossario
├── requisiti/             requisiti funzionali, non funzionali e di conformità
├── architettura/          architettura, Policy Engine, deployment
├── moduli/                MDM, Android, gestione scolastica, Family Control, cyberbullismo
├── sicurezza-privacy/     sicurezza, privacy, quadro normativo
├── decisioni/             Architecture Decision Records (ADR)
└── _en/                   versione inglese (pubblicata sotto /en/)
```

L'**italiano** è la lingua predefinita e la versione di riferimento ([ADR-0007](docs/decisioni/0007-lingue-documentazione.md)). Il rispetto della normativa su privacy e minori è un vincolo bloccante ([ADR-0008](docs/decisioni/0008-conformita-normativa.md)).

## Anteprima in locale

```bash
podman run --rm -v "$PWD/docs:/srv/jekyll:Z" -p 4000:4000 docker.io/jekyll/jekyll:4 \
  sh -c "gem install jekyll-remote-theme jekyll-relative-links jekyll-seo-tag >/dev/null && jekyll serve --host 0.0.0.0"
```

Il sito viene pubblicato automaticamente su GitHub Pages a ogni push su `main` ([workflow](.github/workflows/pages.yml)).

## Contribuire

Leggi [CONTRIBUTING](https://github.com/EduWISP/.github/blob/main/CONTRIBUTING.md) e il [Codice di condotta](https://github.com/EduWISP/.github/blob/main/CODE_OF_CONDUCT.md). Idee e domande in [Discussions](https://github.com/EduWISP/docs/discussions), proposte concrete nelle [Issue](https://github.com/EduWISP/docs/issues).

**Non inserire mai dati personali reali** di studenti, famiglie o personale scolastico: solo esempi fittizi.

## Licenza

La licenza non è ancora stata scelta: vedi [LICENSE-STATUS.md](LICENSE-STATUS.md) e [ADR-0006](docs/decisioni/0006-licenza.md).
