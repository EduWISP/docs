# Deployment e hosting — visione concettuale

## Requisito

Debian GNU/Linux 13 (Trixie) è il sistema operativo di riferimento per il server.

## Modelli

### Cloud hosted
Un'organizzazione o un fornitore ospita il servizio su infrastruttura cloud. Devono essere definiti responsabilità, localizzazione dati, backup, disponibilità e accordi privacy.

### Self-hosted
Un istituto, una rete di scuole o un soggetto incaricato gestisce autonomamente l'infrastruttura. La documentazione futura dovrà descrivere dimensionamento, aggiornamenti, backup, monitoraggio e ripristino.

## Scelte non ancora definite

- runtime e framework;
- database;
- code e processi asincroni;
- reverse proxy;
- containerizzazione o installazione nativa;
- alta affidabilità;
- backup e disaster recovery;
- metriche e logging.

## Principio

Cloud-first descrive una priorità progettuale e un'esperienza di gestione; non significa dipendenza obbligatoria da un cloud proprietario. L'architettura deve restare portabile e documentata.
