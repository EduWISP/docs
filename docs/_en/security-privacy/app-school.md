---
title: EduWISP School app privacy policy
parent: Security & privacy
nav_order: 5
permalink: /en/security-privacy/app-school/
---

# Privacy policy of the «EduWISP School» app

*Last updated: 27 November 2026.* 🇮🇹 [Italiano](/docs/sicurezza-privacy/app-scuola/)

**EduWISP School** (`org.eduwisp.scuola`) is free software (AGPL-3.0-or-later) from the EduWISP project, for school staff: teachers, class coordinators and head teachers. Source code: <https://github.com/EduWISP/eduwisp-app-scuola>.

**Who processes the data.** The app connects to **your school's EduWISP server**, entered at sign-in. The data you see (classes, students, tablets, app requests) is processed by the **school**, which is the data controller: contact the school for its full privacy notice and your rights. The EduWISP project does not receive this data. The test environment `demo.eduwisp.org` contains **fictitious data only**.

**Data used by the app.** The school server address (stored on the phone); username and password (sent only to the school server over HTTPS at sign-in; **the password is not stored**); an access token (stored on the phone, **encrypted** with the Android Keystore; the server keeps only its hash; valid 30 days, revocable); the phone model name (sent to the school server to identify the device in the list of sign-ins); the chosen role and the number of pending requests (on the phone). **No student data is stored on the phone**; notifications show only **how many** requests are pending, without names.

**What the app does not do.** No location, camera, microphone, contacts or file access; no ads, analytics, tracking or third-party services (no Firebase or Google Play Services); no sharing with anyone except the school server; no cloud backup or device transfer.

**Security and retention.** All traffic uses HTTPS. Signing out **revokes** the token on the server; uninstalling the app deletes its data from the phone. Server-side retention follows the school's rules.

**Contact.** EduWISP project: <https://eduwisp.org> · [discussion group](https://groups.google.com/g/eduwisp-sviluppo). For data processed by the school: your school and its data protection officer.
