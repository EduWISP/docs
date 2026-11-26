---
title: Requirements list
parent: Requirements
nav_order: 1
---

# Requirements

The following is a design baseline to be discussed and validated. It does not describe implemented features. Requirement IDs are shared with the Italian version, which is authoritative.

**Status:** `proposed` · `approved` · `rejected` · `on hold`

## Functional requirements

| ID | Requirement | Module | Status |
|---|---|---|---|
| RF-001 | Support multiple schools with logical data separation. | Core | proposed |
| RF-002 | Manage granular roles and permissions. | Core | proposed |
| RF-003 | Represent sites, classes, groups, teachers and students. | School management | proposed |
| RF-004 | Assign and reassign devices through authorised procedures. | MDM | proposed |
| RF-010 | Enroll devices through supported provisioning methods. | MDM | proposed |
| RF-011 | Keep a minimal device and software inventory. | MDM | proposed |
| RF-012 | Assign mandatory and optional apps. | Application Management | proposed |
| RF-013 | Apply managed configurations and compatible restrictions. | MDM | proposed |
| RF-014 | Support educational profiles and temporary modes, if allowed by the provider. | Policy Engine | proposed |
| RF-015 | Record policy synchronisation outcome and date. | MDM | proposed |
| RF-016 | Provide an own app catalogue (signed APKs) for distribution without proprietary stores. | Application Management | proposed |
| RF-017 | Generate provisioning QR codes for the EduWISP DPC. | MDM | proposed |
| RF-020 | Verify the parent/guardian-student relationship. | Family Control | proposed |
| RF-021 | Allow additional family rules within authorised scopes. | Family Control | proposed |
| RF-022 | Show active rules and their origin. | Policy Engine | proposed |
| RF-023 | Prevent family rules from overriding the security baseline. | Policy Engine | proposed |
| RF-030 | Provide a simple, accessible reporting channel. | Cyberbullying | proposed |
| RF-031 | Allow reports from authorised roles. | Cyberbullying | proposed |
| RF-032 | Manage intake, assignment, status and follow-up. | Cyberbullying | proposed |
| RF-033 | Restrict case access by need and role. | Cyberbullying | proposed |
| RF-034 | Keep an audit trail of case views and changes. | Audit | proposed |
| RF-035 | Provide educational and prevention resources. | Cyberbullying | proposed |

## Non-functional requirements

| ID | Requirement | Status |
|---|---|---|
| RNF-001 | Privacy by design and data minimisation. | proposed |
| RNF-002 | Tenant isolation. | proposed |
| RNF-003 | Strong authentication and verifiable authorisation. | proposed |
| RNF-004 | Encrypted communications. | proposed |
| RNF-005 | Audit trail not alterable by ordinary users. | proposed |
| RNF-006 | Support for cloud hosting and self-hosting. | proposed |
| RNF-007 | Documentation of APIs and provider limits. | proposed |
| RNF-008 | Accessibility and usability for students and staff. | proposed |
| RNF-009 | Resilience to intermittent connectivity, within Android limits. | proposed |
| RNF-010 | Backup, restore and incident procedures to be specified. | proposed |
| RNF-011 | Reference server platform: Debian GNU/Linux 13 (Trixie). | approved |
| RNF-012 | All required components are open source and free; no proprietary service in the core (ADR-0009). | approved |
| RNF-013 | Open, documented, versioned server-agents protocol. | proposed |
| RNF-014 | Platform-independent core: new platforms are added with an agent and a profile, without changing core modules (ADR-0011). | approved |
| RNF-015 | Each agent declares its capabilities; non-applicable rules are shown, not ignored. | approved |
| RNF-016 | Works on devices as sold: no bootloader unlocking or modified OS; enrollment only through standard methods (ADR-0003). | approved |

## Compliance requirements

Derived from the [legal framework](../security-privacy/legal-framework.md); binding (ADR-0008).

| ID | Requirement | Status |
|---|---|---|
| RC-001 | No processing of real data before a DPIA, legal review and DPO opinion. | approved |
| RC-002 | Every data item has a documented purpose, legal basis and retention period. | approved |
| RC-003 | Defaults are always the most protective (privacy by default). | approved |
| RC-004 | No student profiling and no automated decisions affecting students. | approved |
| RC-005 | No covert surveillance features (messages, keylogging, screen capture, continuous location). | approved |
| RC-006 | Notices and active-rule views understandable by minors. | approved |
| RC-007 | Data stored in the EU; third-party flows mapped and documented. | approved |
| RC-008 | Data export and deletion per school and per data subject. | approved |
| RC-009 | Tools supporting school obligations: records of processing, notices, DPIA, Art. 28 agreement. | proposed |
| RC-010 | Staff logs and audits compliant with Art. 4 of the Italian Workers' Statute. | approved |
| RC-011 | Interfaces compliant with Italian public-sector accessibility requirements. | proposed |
| RC-012 | No AI feature without a dedicated ADR, AI Act analysis and DPIA; emotion recognition is prohibited. | approved |

## Acceptance criteria

Before development each requirement needs: ID, rationale, stakeholders, priority, dependencies, risks, verifiable criteria and status.
