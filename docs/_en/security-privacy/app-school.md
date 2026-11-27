---
title: EduWISP School app privacy policy
parent: Security & privacy
nav_order: 5
permalink: /en/security-privacy/app-school/
---

# Privacy policy of the «EduWISP School» app

*Last updated: 28 November 2026.* 🇮🇹 [Italiano](/docs/sicurezza-privacy/app-scuola/)

**EduWISP School** (`org.eduwisp.scuola`) is free software (AGPL-3.0-or-later) from the EduWISP project, for school staff: teachers, class coordinators and head teachers. Source code: <https://github.com/EduWISP/eduwisp-app-scuola>.

**Who processes the data.** The app connects to **your school's EduWISP server**, entered at sign-in. The data you see (classes, students, tablets, app requests) is processed by the **school**, which is the data controller: contact the school for its full privacy notice and your rights. The EduWISP project does not receive this data. The test environment `demo.eduwisp.org` contains **fictitious data only**.

**Data used by the app.** The school server address (stored on the phone); username and password (sent only to the school server over HTTPS at sign-in; **the password is not stored**); an access token (stored on the phone, **encrypted** with the Android Keystore; the server keeps only its hash; valid 30 days, revocable); the phone model name (sent to the school server to identify the device in the list of sign-ins); the decisions and reasons a teacher writes on app requests (sent to the school server and kept on record for the coordinator and head teacher); the chosen role and the number of pending requests (on the phone). **No student data is stored on the phone**; notifications show only **how many** requests are pending, without names.

**What the app does not do.** No location, camera, microphone, contacts or file access; no ads, analytics, tracking or third-party services (no Firebase or Google Play Services); no sharing with anyone except the school server; no cloud backup or device transfer.

**Security and retention.** All traffic uses HTTPS. Signing out **revokes** the token on the server; uninstalling the app deletes its data from the phone. Server-side retention follows the school's rules.

## Deleting your data

**EduWISP School** does not create accounts: your account is created and managed by your **school**.

1. **Data on the phone**: tap **Sign out** in the app (this also revokes the token on the server) or uninstall the app. The server address, token and preferences are deleted immediately.
2. **Data on the school server** (account, list of sign-ins, decisions on app requests): ask your school, i.e. its office or data protection officer, to delete it (GDPR art. 17).
3. The school deletes the account and the sign-ins. Decisions on app requests are kept for the period set by its school-records rules, then deleted.

The EduWISP project does not keep data about app users and cannot delete it on the school's behalf.

**Contact.** EduWISP project: <https://eduwisp.org> · [discussion group](https://groups.google.com/g/eduwisp-sviluppo). For data processed by the school: your school and its data protection officer.
