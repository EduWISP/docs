---
title: Android management
parent: Modules
nav_order: 2
---

# Android management

## Target

School-owned Android tablets with Google Mobile Services (proposal: ADR-0003).

## Management mode

Fully Managed / Android Enterprise is the primary scenario to assess. The final choice depends on:
- enrollment and provisioning requirements;
- vendor and Android version support;
- terms of access to Google services;
- API availability and limits;
- sustainability for an open-source project.

## Android Management API

Any integration with Android Management API must be preceded by a formal review of Google's terms, eligibility criteria and permitted use cases. We do not assume an open-source project is automatically granted access. Data flows to Google must be assessed under GDPR rules on international transfers.

## Provider abstraction

EduWISP's data model and policies should be provider-independent. An adapter translates canonical intents into supported features and explicitly reports unavailable ones.

## Compatibility matrix

Before development we must fill in the [compatibility matrix](android-compatibility-matrix.md) for each feature: supported, partial, unsupported, vendor/version dependent, or to be verified.
