---
title: Policy Engine
parent: Architecture
nav_order: 2
---

# Policy Engine

## Purpose

Define, combine and explain the rules governing the device in different contexts.

## Policy dimensions

- target subject and device;
- tenant, school, site, class or group;
- scope (security, education, family);
- period and calendar;
- origin and owner;
- priority and rationale;
- required features and provider compatibility.

## Composition principles

The security baseline cannot be weakened by less-privileged policies. Mandatory educational policies must be recognisable. Family policies may add limits within their scope but cannot override security or mandatory education.

## Effective result

The system should show:
- the applied rule;
- its source;
- its rationale;
- any conflict;
- device/provider compatibility;
- distribution status and last sync.

## Offline

Already-distributed policies may stay active without network, if the provider allows it. The design must define expiry, trusted clock, fail-safe behaviour and handling of stale policies.
