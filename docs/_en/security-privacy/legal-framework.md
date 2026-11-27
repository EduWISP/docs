---
title: Legal framework
parent: Security & privacy
nav_order: 3
---

# Legal framework

EduWISP processes data of **minors** in a **school** context, often on behalf of **public bodies**. Compliance with Italian and EU law is a **blocking constraint** (ADR-0008).

{: .important }
> This page is a working list for design purposes, **not legal advice**. The [Italian version](/docs/sicurezza-privacy/quadro-normativo/) is authoritative. Every reference must be checked against the texts in force and validated with the school's DPO and qualified advisers before processing real data.

## Data protection

| Law | Impact on EduWISP |
|---|---|
| **GDPR (Reg. (EU) 2016/679)** Art. 5 | Lawfulness, minimisation, purpose and storage limitation, integrity and confidentiality, accountability. |
| GDPR Art. 6 and 9 | For state schools the usual legal basis is a task in the public interest or a legal obligation, not consent. Cyberbullying reports may involve special-category or highly sensitive data. |
| GDPR Art. 8, Recital 38 | Children merit specific protection. In Italy the digital consent age is **14** (Art. 2-quinquies, Italian Privacy Code). |
| GDPR Art. 12-14 | Notices clear and **understandable for a child**. |
| GDPR Art. 22 | No solely automated decisions with significant effects on students. |
| GDPR Art. 25 | Privacy by design and by default. |
| GDPR Art. 28 | Whoever hosts/operates EduWISP for a school is a **processor** and needs a data processing agreement. |
| GDPR Art. 30, 32, 33-34 | Records of processing, appropriate security, breach notification (72 hours to the authority when required). |
| GDPR Art. 35 | A **DPIA** is likely required (vulnerable data subjects, device monitoring, cyberbullying reports). |
| GDPR Art. 37-39 | Public schools must have a **DPO**, to be involved from the design stage. |
| GDPR Art. 44+ | Non-EU transfers only with appropriate safeguards; goal: **data in the EU**; flows to Google services to be assessed. |
| **Italian Privacy Code** (Legislative Decree 196/2003, as amended by Legislative Decree 101/2018) | Art. 2-ter, 2-quinquies, 2-sexies. |
| **Italian DPA (Garante) guidance** | School-specific guidance and decisions. |

## Minors and cyberbullying

| Law | Impact on EduWISP |
|---|---|
| **UN Convention on the Rights of the Child** (Italian Law 176/1991) | The child's **best interests** guide every design choice; right to privacy (Art. 16). |
| **Law 71/2017** on cyberbullying, amended by **Law 70/2024** | School contact person, family information duties, reporting procedures. |
| **Ministry of Education guidelines** on bullying and cyberbullying | Operational guidance for schools. |

## Age of minors

Each student's age is computed from their **date of birth**, never from their class: a student who repeated a year can be older than their classmates. *Checked on 28 November 2026.*

| Age | Law | What it means for EduWISP |
|---|---|---|
| **14** | Art. 2-quinquies of the Italian Privacy Code (Legislative Decree 101/2018), derogating from GDPR art. 8 | From 14 a minor can consent to information society services; under 14 the holder of parental responsibility consents. Notices for minors must be clear and age-appropriate. |
| **14** | Law 132/2025 on artificial intelligence, art. 4(4) (in force since 10 October 2025) | Under 14, access to AI systems requires parental consent; from 14 the minor can consent if the information is understandable. |
| **14** | Law 71/2017 on cyberbullying | A minor aged 14 or over can request takedown of content directly. |
| **16** | GDPR art. 8 | Default digital consent age where a Member State has not lowered it (minimum 13). Italy uses 14; installations in other countries can configure it (`EDUWISP_DIGITAL_CONSENT_AGE`). |
| **18** | Italian Civil Code, art. 2 | Parental responsibility ends: in EduWISP family members lose access unless the student consents on the tablet (ADR-0018). |

**Proposals not yet law** (to follow): amendments and bills on minors' access to social media (ban under 13, account linked to a parent's until 15 or 16). They do not change EduWISP, where social media apps are already blocked on student tablets (ADR-0019), but must be checked if passed.

## Artificial intelligence

| Law | Impact on EduWISP |
|---|---|
| **EU AI Act (Reg. (EU) 2024/1689)** Art. 5 | Emotion recognition in education is **prohibited** (save medical/safety exceptions). |
| AI Act Annex III, point 3 | AI in education is **high-risk**, including systems monitoring prohibited student behaviour during tests. |
| **Italian Law 132/2025** on AI | Specific provisions on minors, including parental consent for under-14s accessing AI. |

No AI feature is in the initial scope.

## Workers (teachers and staff)

| Law | Impact on EduWISP |
|---|---|
| **Workers' Statute (Law 300/1970)** Art. 4 | Logs and audits on staff actions may constitute remote monitoring: limits, notice and, where required, union procedures. |

## Public administration

| Law | Impact on EduWISP |
|---|---|
| **Digital Administration Code** (Legislative Decree 82/2005) Art. 68-69, AgID guidelines | Public bodies must consider open-source and reusable software (Developers Italia catalogue). |
| **Law 4/2004** and AgID accessibility guidelines | Accessible interfaces (EN 301 549 / WCAG). |
| **ACN cloud qualification** | Cloud offers for state schools must meet public-sector qualification requirements. |

## Resulting project rules

1. **No real data** before DPIA, legal review and DPO approval.
2. **Minimisation:** documented purpose, legal basis and retention for each data item.
3. **No profiling**, rankings or behavioural scores of students.
4. **No automated decisions** affecting students; human oversight always.
5. **No covert surveillance.**
6. **Transparency towards the child**, in age-appropriate language.
7. **Data in the EU**, third-party flows mapped.
8. **Support for school obligations**: records, notices, DPIA, processor agreement templates.

## Italian Data Protection Authority guidance for schools

From the Garante's [FAQ "Scuola e privacy"](https://www.gpdp.it/home/faq/scuola-e-privacy) and the 2023 handbook ["La scuola a prova di privacy"](https://www.gpdp.it/scuola): health, disability and learning-disorder (DSA) data are known only to entitled people and never disclosed; students with DSA may use the tools in their personal learning plan (recorders, computers) even where recording is otherwise banned; general communications must not identify pupils (disability, health, bullying, sanctions); schools are controllers and must provide a privacy notice. For EduWISP: per-student app exceptions without any stated reason, notifications only to the people concerned, no surveillance through device cameras, microphones or screens, and a privacy-notice template.
