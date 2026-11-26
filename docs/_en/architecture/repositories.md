---
title: Repository layout
parent: Architecture
nav_order: 4
---

# Repository layout

Every module has its own repository, so that someone can take ownership of it independently (ADR-0010). The model is inspired by [OpenWISP](https://github.com/openwisp). The [Italian page](/docs/architettura/repository/) is authoritative.

{: .note }
> Names are a proposal. Repositories will be created when each module enters development.

## Repository map

| Repository | Content | OpenWISP equivalent |
|---|---|---|
| `eduwisp-utils` | Shared utilities, QA, common UI components | `openwisp-utils` |
| `eduwisp-users` | Core & Identity: tenants, users, roles, multi-tenancy | `openwisp-users` |
| `eduwisp-audit` | Audit log and minimised reporting | — |
| `eduwisp-school` | Schools, sites, classes, teachers, students | — |
| `eduwisp-devices` | MDM: inventory, lifecycle, commands, provisioning | `openwisp-controller` |
| `eduwisp-policy` | Policy Engine | — |
| `eduwisp-apps` | App catalogue (signed APKs), assignments, managed configurations | — |
| `eduwisp-family` | Family Control | — |
| `eduwisp-wellbeing` | Cyberbullying case management and digital wellbeing | — |
| `eduwisp-protocol` | Open, versioned server-agent protocol spec, schemas, conformance tests | `netjsonconfig` / NetJSON |
| `eduwisp-android-dpc` | Open-source EduWISP DPC (*device owner*), first agent | `openwisp-config` |
| `eduwisp-desktop-agent` | Windows/macOS/Linux agent for Family Control (to be created, ADR-0014) | — |
| `eduwisp-family-android` | Family Control app for personal Android devices, no device owner (to be created) | — |
| `eduwisp-<platform>-agent` | Agents for other platforms, in the future (ADR-0011) | `openwrt-openwisp-monitoring` |
| `ansible-eduwisp` | Install and upgrade on Debian 13 | `ansible-openwisp2` |
| `docker-eduwisp` | Container images and composition | `docker-openwisp` |
| `.github` | Profile, community files, templates, reusable workflows | `.github` |
| `docs` | Design, ADRs, site aggregating all module docs | `openwisp-docs` |

## Rules

- Separate repositories do **not** mean microservices: server modules combine into one installable application, as in OpenWISP.
- Dependencies point **one way**, towards the base modules (`utils`, `users`); no cycles.
- Modules interact **only through documented interfaces** (APIs, events, extension points).
- Server and agents both depend on the multi-platform `eduwisp-protocol`, not on each other.
- `eduwisp-wellbeing` handles the most sensitive data: separate domain, restricted access.

## Minimum structure of each repository

`README.md`, `docs/user/` and `docs/developer/` (aggregated into the site), `CHANGES.md`, `LICENSE`, `CODEOWNERS`, `publiccode.yml` (for the Italian public-sector reuse catalogue, Developers Italia), `tests/`, CI via the organisation's reusable workflows, and `PRIVACY.md` describing the personal data processed. Community files are inherited from `.github`.

## Releases

Each module uses semantic versioning. Periodic **platform releases** pin a tested combination of module versions.

## Module owners

Propose taking ownership of a module in [Discussions](https://github.com/EduWISP/docs/discussions); owners are listed in `CODEOWNERS` and in the governance page.
