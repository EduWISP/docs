---
title: Server architecture
parent: Architecture
nav_order: 5
---

# Server architecture

Decided in ADR-0016; the [Italian page](/docs/architettura/server/) is authoritative.

**Status (27 Nov 2026, `server.eduwisp.org`, demo with fictitious data):** nginx/TLS with rate limiting, Django/gunicorn, PostgreSQL, Valkey + Celery, BorgBackup with monthly restore test (remote archive pending), Monit and daily security summary with email alerts, platform-release upgrades with automatic rollback, 90-day logs, firewall, fail2ban, Suricata, AIDE, auditd and hardening (Lynis 78/100) are **running**. Still to do: `/health/`, MFA, data separation design.

- **Single Debian 13 VM to start, ready to grow:** nginx (TLS, static files, rate limiting), Django + gunicorn (UI and API, stateless), PostgreSQL 17, Valkey (local-only message broker), Celery worker and beat; each service with its own user and systemd sandboxing.
- **Data separation:** Family Control in a separate database (possibly another server); cyberbullying data in a separate PostgreSQL schema with a dedicated role and application-level encryption of sensitive fields; disk encryption recommended in production.
- **Backups:** BorgBackup, encrypted, remote, append-only; nightly database dump and configuration; retention 7 daily / 4 weekly / 6 monthly; automatic monthly restore test. Targets: max 24 h data loss, restore within 4 h.
- **Updates:** automatic Debian security patches; EduWISP upgrades to a platform release (pinned module commits) with a separate `aggiorna.yml` playbook: restore point (Borg, database dump, venv and project copies) → maintenance page (HTTP 503) → install → migrate → verify. Any failure triggers an **automatic rollback** (database recreated from the dump), a check and an email alert.
- **Monitoring:** `/health/` endpoint, Monit (services, disk, certificate expiry), daily Suricata and AIDE summaries, email alerts via SMTP relay; logs kept 90 days, admins only. Prometheus/Grafana optional for large installations.
- **Sizing (to be validated by load tests):** up to 500 devices: 2 vCPU / 4 GB / 40 GB; up to 3,000: 4 vCPU / 8 GB / 100 GB SSD; up to 20,000: separate app (8 vCPU, 16 GB) and PostgreSQL (4 vCPU, 16 GB) VMs.
