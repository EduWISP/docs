---
title: EduWISP Family app privacy policy
parent: Security & privacy
nav_order: 6
permalink: /en/security-privacy/app-family/
---

# Privacy policy of the «EduWISP Family» app

*Last updated: 28 November 2026.* 🇮🇹 [Italiano](/docs/sicurezza-privacy/app-famiglia/)

**EduWISP Family** (`org.eduwisp.famiglia`) is free software (AGPL-3.0-or-later) from the EduWISP project, for parents and guardians of students. Source code: <https://github.com/EduWISP/eduwisp-app-famiglia>.

**Who processes the data.** The app connects to **your school's EduWISP server**, entered at sign-in. The data you see about your children (class, school tablet, allowed apps, app requests) is processed by the **school**, which is the data controller: contact the school for its full privacy notice and your rights. The EduWISP project does not receive this data. The test environment `demo.eduwisp.org` contains **fictitious data only**.

**What you see.** **Only your own children**, with the same permissions as the school web portal. Once your child comes of age, you see their data only if they allow it from their tablet; otherwise you only see that they are of age.

**Data used by the app.** The school server address (stored on the phone); username and password (sent only to the school server over HTTPS at sign-in; **the password is not stored**); an access token (stored on the phone, **encrypted** with the Android Keystore; the server keeps only its hash; valid 30 days, revocable); the phone model name (sent to the school server to identify the device in the list of sign-ins); your opinion on app requests with its reason (sent to the school server, recorded and visible to teachers, the class coordinator and the head teacher); the chosen role and the number of requests waiting for your opinion (on the phone). **No data about your children is stored on the phone**; notifications show only **how many** requests are waiting, without names.

**What the app does not do.** No location, camera, microphone, contacts or file access; no ads, analytics, tracking or third-party services (no Firebase or Google Play Services); no sharing with anyone except the school server; no cloud backup or device transfer; it does not control your children's phones (family control on family devices will be a separate optional module).

**Security and retention.** All traffic uses HTTPS. Signing out **revokes** the token on the server; uninstalling the app deletes its data from the phone. Server-side retention follows the school's rules.

## Deleting your data

**EduWISP Family** does not create accounts: your account is created and managed by the **school**.

1. **Data on the phone**: tap **Sign out** in the app (this also revokes the token on the server) or uninstall the app. The server address, token and preferences are deleted immediately.
2. **Data on the school server** (account, list of sign-ins, opinions on app requests): ask the school, i.e. its office or data protection officer, to delete it (GDPR art. 17).
3. The school deletes the account and the sign-ins. Opinions on app requests are kept for the period set by its school-records rules, then deleted.

The EduWISP project does not keep data about app users and cannot delete it on the school's behalf.

**Contact.** EduWISP project: <https://eduwisp.org> · [discussion group](https://groups.google.com/g/eduwisp-sviluppo). For data processed by the school: the school and its data protection officer.
