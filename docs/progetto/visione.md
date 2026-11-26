---
title: Visione e perimetro
parent: Progetto
nav_order: 1
---

# Visione, obiettivi e perimetro

## Visione

Costruire una piattaforma aperta che aiuti gli istituti a gestire i dispositivi digitali didattici con strumenti centralizzati, regole comprensibili e tutela degli studenti.

## Obiettivi

1. Gestire in modo centralizzato tablet di proprietà scolastica.
2. Distribuire applicazioni e configurazioni didattiche.
3. Organizzare dispositivi per istituto, plesso, classe e studente.
4. Coordinare policy scolastiche e familiari.
5. Supportare prevenzione e gestione di segnalazioni di cyberbullismo.
6. Garantire portabilità, documentazione e possibilità di self-hosting.
7. Ridurre al minimo i dati personali trattati.

## Perimetro iniziale

- Tablet Android di proprietà della scuola, con o senza servizi Google (vedi ADR-0003).
- Dispositivi di proprietà della scuola (school-owned).
- Gestione Fully Managed tramite un DPC EduWISP open source.
- Solo componenti open source e gratuiti (ADR-0009).
- Server Debian GNU/Linux 13 Trixie.
- Multi-tenancy per più istituti.

## Evoluzione prevista

L'architettura è indipendente dalla piattaforma ([ADR-0011](../decisioni/0011-multipiattaforma.md)): in futuro potranno essere integrati dispositivi diversi da Android tramite nuovi agenti.

## Fuori perimetro iniziale


- Gestione BYOD come scenario primario.
- Sorveglianza generalizzata della vita privata.
- Sostituzione dei servizi di emergenza, dei servizi sociali o delle procedure scolastiche ufficiali.
- Decisioni disciplinari automatizzate.
