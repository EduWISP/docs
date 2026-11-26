---
title: Android compatibility matrix
parent: Modules
nav_order: 3
---

# Android compatibility matrix

Compares the two technical options for managing school-owned **Fully Managed** tablets. The [Italian page](/docs/moduli/android-matrice-compatibilita/) is authoritative.

- **AMAPI**: Google's Android Management API with the Android Device Policy app. **Proprietary: excluded from the core by ADR-0009, kept for comparison only.**
- **EduWISP DPC**: an open-source project app installed as *device owner*, using Android's `DevicePolicyManager` APIs directly. **Primary approach.**

**Legend:** ✅ documented · 🟡 partial/limited · ❌ not available · ❔ not confirmed · ⚠️ blocking constraint

{: .important }
> Official documentation checked on **2026-11-26**. Nothing has been **tested on real devices** yet.

## 1. Access conditions

| Aspect | AMAPI | EduWISP DPC |
|---|---|---|
| Who can use it | ⚠️ Restricted to commercial EMM developers, Device Trust providers and OEMs, with a direct agreement with end customers | Android (AOSP) APIs, open to anyone |
| Quotas | ⚠️ Initial quota up to 500 devices with full business justification; max 2 projects per developer | None |
| Google approval | Part of quota access | ⚠️ Since 2025 only DPCs verified by Android Enterprise may be installed during enrollment; others are blocked by Play Protect. The approval process for new DPCs is not publicly documented |
| Cost | No cost stated | Free |
| Managed Google Play | ✅ Included | ❌ New custom DPC registrations to the Play EMM API are closed; own APK catalogue only |
| Data flows | ⚠️ Device data processed by Google; location not stated | Data stays on EduWISP servers (EU, self-hosting) |
| Self-hosting | 🟡 Each instance would need its own approved Google project | ✅ |

## 2. Features

| Feature | AMAPI | EduWISP DPC | Notes |
|---|---|---|---|
| QR provisioning | ✅ Android 7.0+ | ⚠️ Supported by APIs, but blocked on GMS devices if the DPC is not approved | Android 12+: `ACTION_GET_PROVISIONING_MODE`, `ACTION_ADMIN_POLICY_COMPLIANCE` |
| Zero-touch | ✅ Android 8.0+, authorised reseller | ❔ | |
| Mandatory apps | ✅ `FORCE_INSTALLED`, `REQUIRED_FOR_SETUP` | ✅ Silent install by device owner (`PackageInstaller`) | DPC: own APKs only |
| Optional apps | ✅ `AVAILABLE` via managed Play | 🟡 Own catalogue only | |
| Block non-allowed apps | ✅ `playStoreMode` allowlist, `BLOCKED` | ✅ `setApplicationHidden`, `setPackagesSuspended`, `setUninstallBlocked` | |
| Managed configurations | ✅ `managedConfiguration` | ✅ `setApplicationRestrictions` | |
| Single-app kiosk | 🟡 `KIOSK` (deprecated) | ✅ Lock task, Android 5.0+ | |
| Multi-app kiosk (test mode) | ✅ `kioskCustomLauncherEnabled` | ✅ `setLockTaskPackages`, `setLockTaskFeatures` (Android 9+) | |
| Restrictions | ✅ camera, microphone, screen capture, factory reset, USB, developer settings, … | ✅ `DISALLOW_*` user restrictions, `setCameraDisabled`, `setScreenCaptureDisabled` | |
| Wi-Fi | ✅ ONC | ❔ | |
| Certificates | 🟡 | ✅ `installCaCert`, `installKeyPair` | |
| System updates | ✅ automatic/windowed/postpone, freeze periods | ✅ `SystemUpdatePolicy` (Android 6.0+), freeze periods (Android 9+) | |
| Remote lock | ✅ `LOCK`, lost mode | ✅ `lockNow` | |
| Remote reboot | ✅ `REBOOT` | ❔ | |
| Remote wipe | ✅ `WIPE` | ✅ `wipeData` / `wipeDevice` | High-impact action |
| Clear app data | ✅ `CLEAR_APP_DATA` (Android 9+) | ❔ | |
| Inventory | ✅ opt-in via `statusReportingSettings` | ✅ | **Minimise**: `networkInfo` includes IMEI and MAC |
| Status and last sync | ✅ | ✅ To be implemented | |
| Time-slot policies (school/home) | 🟡 No native scheduling; server must switch policies, needs connectivity | ✅ Local logic, works offline | Key for Family Control |
| Per-app time limits | ❌ Not found | 🟡 Via `setPackagesSuspended` + usage stats (to be confirmed) | |
| Offline behaviour | 🟡 Re-provisioning after 270 days offline | 🟡 Implementation-dependent; trusted clock needed | |

## 3. What follows

With ADR-0009 the AMAPI column is for comparison only. The project must build the free alternatives:

| Proprietary function | EduWISP alternative |
|---|---|
| Android Device Policy | **EduWISP DPC**, open source, device owner |
| Android Management API | **EduWISP server** with an open server-agent protocol |
| Managed Google Play | **EduWISP app catalogue** of signed APKs (F-Droid-like) |
| Zero-touch portal | **QR provisioning** from the EduWISP server; zero-touch to be verified |

Open issues: ⚠️ DPC approval on GMS devices (see ADR-0003); Play-only apps; ❔ rows; real-device tests.

## Sources

See the [Italian page](/docs/moduli/android-matrice-compatibilita/#fonti).
