---
title: Family Control
parent: Modules
nav_order: 5
---

# Family Control

A **free, open-source** parental control integrated with the school's rules. It is **optional**: only the parent or guardian can turn it on (ADR-0014). The [Italian page](/docs/moduli/family-control/) is authoritative.

## Two coordinated scopes (ADR-0002)

The school governs the school tablet (security, education); parents can add rules for home use, without overriding security or mandatory education.

## Devices

| Device | How | Status |
|---|---|---|
| School tablet | Family rules applied by the EduWISP DPC | Planned |
| Family Android phones and tablets | `eduwisp-family-android` app, **no factory reset** | Planned |
| Windows PC | `eduwisp-desktop-agent` | Planned (signing via SignPath Foundation, to apply) |
| macOS | `eduwisp-desktop-agent` | **Planned for a later phase** |
| Linux PC | `eduwisp-desktop-agent` | Planned |
| iPhone, iPad | — | **Planned for a later phase** |

## Features

**Planned:** daily time limits, time slots, web content filtering by category, allowed/blocked apps, aggregated usage summaries visible to the child too, extra-time requests, instant pause.

**Excluded:** reading messages, chats or email; keylogging; screenshots or screen recording; call recording; continuous location tracking.

## Principles

Parent's explicit choice (can be turned off anytime, never imposed by the school); data separated from the school; transparency towards the child with age-appropriate defaults; no copying of commercial products' names, brands or interfaces.

## Open points

Data controllership, separated parents, involvement of children aged 14+, Apple support: see ADR-0014.
