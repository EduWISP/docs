---
title: Decisions (ADR)
nav_order: 7
---

# Decision log (summary)

ADRs are written in Italian (ADR-0007). This is an English summary; follow the links for the full text.

| ADR | Decision | Status |
|---|---|---|
| [0001](/docs/decisioni/0001-uso-degli-adr/) | Record design decisions as ADRs | Accepted |
| [0002](/docs/decisioni/0002-modello-scuola-famiglia/) | Two coordinated scopes: school governs security and education, family adds rules for home use | Accepted |
| [0003](/docs/decisioni/0003-target-android/) | Android target and approach: open-source EduWISP DPC, own app catalogue; devices stay as sold (no unlocking); open risk: DPC approval on GMS devices, main path is Android Enterprise verification | Proposed |
| [0004](/docs/decisioni/0004-debian-13-server/) | Debian GNU/Linux 13 as reference server platform | Accepted |
| [0005](/docs/decisioni/0005-cloud-first-self-hostable/) | Cloud-first but always self-hostable | Accepted |
| [0006](/docs/decisioni/0006-licenza/) | Licences: AGPL-3.0-or-later with attribution and trademark terms (code), CC BY-SA 4.0 (docs), name and logo excluded; DCO for contributions | Accepted |
| [0007](/docs/decisioni/0007-lingue-documentazione/) | Bilingual documentation, Italian default and authoritative | Accepted |
| [0008](/docs/decisioni/0008-conformita-normativa/) | Legal compliance (minors, GDPR, Italian law) is a blocking constraint | Accepted |
| [0009](/docs/decisioni/0009-solo-software-libero/) | Only open-source, free-of-charge components; build alternatives to proprietary services | Accepted |
| [0010](/docs/decisioni/0010-un-repository-per-modulo/) | One repository per module, so each can be owned independently | Accepted |
| [0014](/docs/decisioni/0014-family-control-facoltativo-multipiattaforma/) | Optional, parent-chosen Family Control: open-source parental control for the school tablet and family devices (Android, Windows, Linux first; Apple planned for a later phase); data separated from the school; no covert surveillance | Accepted (principles) |
| [0015](/docs/decisioni/0015-ambienti-del-progetto/) | Environments: server.eduwisp.org; demo with fictitious data only; pilot with real data only after DPIA, legal entity, Art. 28 agreements, ACN check and EU hosting | Accepted |
| [0016](/docs/decisioni/0016-architettura-del-server/) | Server architecture: single VM ready to scale, Celery + Valkey, separated Family and cyberbullying data, BorgBackup, platform-release upgrades, Monit monitoring, sizing | Accepted |
| [0017](/docs/decisioni/0017-server-di-backup/) | Dedicated backup server on Debian stable: append-only Borg, client-side encryption, Ansible role then ISO | Accepted |
| [0018](/docs/decisioni/0018-interfaccia-per-ruoli/) | Role-based interface: system admin managing all schools and platform settings, head teacher, teacher, family; server-side permissions, family with one main contact and an optional second, read-only "view as" for admins; adult students decide on their tablet whether families keep access | Accepted |
| [0019](/docs/decisioni/0019-app-consentite/) | App allowlist (platform and school catalogues), apps forbidden everywhere (social, VPN, Tor), school-chosen required apps, audited temporary unlocks, VPN and private DNS locked | Accepted |
| [0020](/docs/decisioni/0020-app-obbligatorie/) | Required apps flagged in the single allowlist, app logos, silent install from school-uploaded APKs (no managed Google Play) | Accepted |
| [0013](/docs/decisioni/0013-stack-tecnologico/) | Tech stack: Python 3.13 + Django 5.2 LTS, DRF, PostgreSQL 17, Celery + Valkey, HTMX + Bootstrap Italia; Kotlin agent with no Google Play Services, UnifiedPush | Accepted |
| [0012](/docs/decisioni/0012-responsabile-del-progetto/) | Project lead: Michele Salerno (final say on decisions, appoints module owners, owns the EduWISP name and logo) | Accepted |
| [0011](/docs/decisioni/0011-multipiattaforma/) | Platform-independent core: Android is the first agent, other platforms can be added via new agents and protocol profiles | Accepted |
