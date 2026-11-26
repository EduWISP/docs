---
title: Deployment and hosting
parent: Architecture
nav_order: 3
---

# Deployment and hosting — concept

## Requirement

Debian GNU/Linux 13 (Trixie) is the reference server operating system (ADR-0004, ADR-0005).

## Models

### Cloud hosted
An organisation or provider hosts the service in the cloud. Responsibilities, data location (EU), backup, availability and data-processing agreements must be defined. Offers for Italian state schools must meet public-sector cloud qualification requirements.

### Self-hosted
A school, school network or appointed party runs the infrastructure. Future documentation will cover sizing, updates, backup, monitoring and recovery.

## Open choices

- runtime and framework;
- database;
- queues and async processing;
- reverse proxy;
- containers or native install;
- high availability;
- backup and disaster recovery;
- metrics and logging.

## Principle

Cloud-first is a design priority and a management experience; it does not mean mandatory dependency on a proprietary cloud. The architecture must remain portable and documented.
