---
title: Roadmap
parent: Project
nav_order: 2
---

# Roadmap

The roadmap describes design phases; it does not state dates or release commitments.

| Phase | Activity | Status |
|---|---|---|
| 1 | Vision and scope | Being defined |
| 2 | Functional and non-functional requirements | To be validated |
| 3 | School-family model | Agreed (ADR-0002) |
| 4 | Cyberbullying & Digital Wellbeing requirements | To be detailed |
| 5 | Logical architecture and domains | Proposed |
| 6 | Formal assessment of Android capabilities | Docs checked, device tests pending ([matrix](../modules/android-compatibility-matrix.md)) |
| 7 | Security, privacy and DPIA | To be detailed |
| 8 | Governance and licence choice | Decided (ADR-0006, ADR-0012) |
| 9 | Technical specifications | Not started |
| 10 | Development | Not started |

## Environments

- **Now:** `demo.eduwisp.org` on `server.eduwisp.org`, fictitious data only.
- **After legal requirements:** `pilota.eduwisp.org` with participating schools (ADR-0015).

## Server installation: order of work

1. **Server architecture** (ADR to be written): components, flows, data, backup, updates, monitoring, sizing.
2. **`ansible-eduwisp` role** completed accordingly.
3. **Installation ISO**, last: Proxmox-style guided installer (disk, network/IP, hostname, admin email, password), EduWISP logo, based on the official signature-verified **Debian stable** installer, **rebuilt automatically** by a scheduled GitHub Action whenever a new Debian stable release is published, with a first-boot wizard running the Ansible role.

## Planned for later phases

- **Family Control on Apple devices** (macOS, iPhone, iPad), requiring Apple's Family Controls entitlement and the Apple Developer Program (ADR-0014).

## Goal: Google Summer of Code

The project aims to apply as a GSoC mentoring organisation. Requirements (2026): OSI-licensed released software, at least 18 months of history, a community with mentors, an AI-use policy. Realistic target: **GSoC 2029**, or earlier via an umbrella organisation.

## Exit criteria for the design phase

- Priority requirements approved.
- Android compatibility matrix verified.
- Roles and responsibilities model approved.
- Privacy and security analysis completed at design level.
- Legal framework validated by a DPO and legal advisers; preliminary DPIA drafted.
- Licence and governance defined.
- Technical architecture justified and documented.
