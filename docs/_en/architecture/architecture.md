---
title: Conceptual architecture
parent: Architecture
nav_order: 1
---

# Conceptual architecture

## Principles

- Separation of functional domains.
- Core independent of the MDM provider.
- Only open-source, free components; no proprietary cloud service in the core (ADR-0009).
- Documented, versioned APIs.
- Multi-tenancy and data isolation.
- Cross-cutting audit and authorisation.
- Modular evolution without premature microservices.

## Logical domains

1. **Core & Identity:** tenants, users, roles, groups and permissions.
2. **School Management:** schools, sites, classes, teachers and students.
3. **Device Management:** inventory, lifecycle and assignments.
4. **Provider Adapter:** translation between the canonical model and the Android provider.
5. **Application Management:** app catalogue and assignments.
6. **Policy Engine:** rule composition and evaluation.
7. **Family Control:** delegations and family policies.
8. **Cyberbullying & Wellbeing:** reports and case management.
9. **Audit & Reporting:** administrative events and minimised reports.
10. **Presentation & API:** portals and integrations.

## Conceptual diagram

```text
School Portal     Family Portal     Student Reporting
      |                 |                    |
      +-----------------+--------------------+
                        |
                 Identity & Core
                        |
       +----------------+-------------------+
       |                |                   |
 School Management  Family Control   Case Management
       |                |                   |
       +----------------+-------------------+
                        |
                   Policy Engine
                        |
                Device Management
                        |
                 Provider Adapter
                        |
           Open server ↔ agent protocol
                        |
      EduWISP DPC (device owner) + app catalogue
```

## Repositories

Each domain maps to one or more independent repositories (ADR-0010). See [Repository layout](repositories.md).

## Technology assumptions

Framework, database, codebase and runtime are not decided yet. The choice will consider community skills, maintainability, security, accessibility, cost and Debian 13 support.

## Multi-tenancy

The design must define tenant boundaries, query isolation, platform administrators, data export and deletion, audit and backup. Isolation must be verifiable and testable.
