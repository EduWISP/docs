---
title: Home (English)
nav_order: 1
permalink: /en/
---

# EduWISP
{: .fs-9 }

Open-source platform for managing school-owned Android devices.
{: .fs-6 .fw-300 }

[Read the vision](project/vision.md){: .btn .btn-primary .mr-2 }
[Join the discussion](https://github.com/EduWISP/docs/discussions){: .btn .mr-2 }
[Italiano](/docs/){: .btn }

---

{: .warning }
> **Status: design phase.** This documentation describes ongoing design work. There is no working product yet and no installation instructions.

{: .note }
> Italian is the project's default language and the **authoritative version**. If the two versions differ, the Italian one prevails.

## What EduWISP is

EduWISP is a proposal for an open-source platform combining **Mobile Device Management (MDM)**, **school management**, **Family Control** and **cyberbullying prevention** tools, inspired by the modularity and philosophy of [OpenWISP](https://openwisp.org/).

## Documentation map

| Section | Content |
|---|---|
| [Project](project/index.md) | Vision, scope, roadmap, governance |
| [Requirements](requirements/index.md) | Functional, non-functional and compliance requirements |
| [Architecture](architecture/index.md) | Logical domains, Policy Engine, deployment |
| [Modules](modules/index.md) | MDM, Android, school management, Family Control, cyberbullying |
| [Security & privacy](security-privacy/index.md) | Security principles, privacy, legal framework |
| [Decisions (ADR)](decisions.md) | Summary of design decisions |

## Principles

- **Open source**, modular, documented APIs.
- **Cloud-first but self-hostable**: no mandatory dependency on a proprietary cloud.
- **Multi-tenancy**: data separated between schools.
- **Privacy by design**: data minimisation, no student surveillance.
- **Legal compliance is a blocking constraint**: we are dealing with minors.
- **Human oversight** for reports and interventions.
- **Transparency** of rules and traceability of administrative actions.

## School-family model

The school keeps institutional control of the device. Families can add extra rules for home use, but cannot disable security policies or block mandatory educational activities.
