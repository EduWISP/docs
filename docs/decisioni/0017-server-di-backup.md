---
title: "ADR-0017: Server di backup dedicato"
parent: Decisioni (ADR)
nav_order: 17
---

# ADR-0017: Server di backup dedicato

- **Stato:** Accettata
- **Data:** 2026-11-27

## Contesto

L'[ADR-0016](0016-architettura-del-server.md) prevede backup cifrati con BorgBackup verso un archivio **remoto in sola aggiunta**. Finora l'archivio stava sulla stessa VM del server, quindi non proteggeva da un guasto del server né da un attacco. Un NAS commerciale (per esempio Synology) richiede pacchetti di terze parti o container per Borg, e la configurazione non è riproducibile con Ansible. Le scuole hanno bisogno di qualcosa che si installi da sé, come il resto di EduWISP.

## Decisione

1. **Server di backup dedicato**, separato dal server EduWISP: una VM o un piccolo computer con **Debian stable**, installato con un ruolo Ansible nel nuovo repository **`ansible-eduwisp-backup`**. In seguito ci sarà anche una **ISO di installazione** in stile Proxmox Backup Server, costruita con lo stesso sistema della ISO del server principale.
2. **BorgBackup in sola aggiunta:** ogni server EduWISP ha una propria chiave SSH, limitata nel file `authorized_keys` a `borg serve --append-only --restrict-to-repository` sul proprio archivio. Un server compromesso non può leggere gli archivi degli altri né cancellare i propri.
3. **Cifratura sul client:** gli archivi sono cifrati dal server EduWISP (`repokey-blake2`); il server di backup **non conosce le passphrase** e non può leggere i dati.
4. **Spazio libero recuperato solo sul server di backup:** le cancellazioni chieste dai client (`borg prune`) diventano effettive solo con `borg compact` eseguito sul server di backup, una volta al mese, dopo un controllo di integrità (`borg check`). Fino ad allora un archivio cancellato per errore o da un attaccante si può recuperare.
5. **Disco dati separato** dal disco di sistema, con LVM, per poterlo ingrandire o sostituire; indicato con il suo identificativo stabile (`/dev/disk/by-id/...`).
6. **Stessa sicurezza del server principale:** hardening, SSH solo con chiavi, firewall nftables che accetta solo i server EduWISP autorizzati e la rete di amministrazione, fail2ban, AIDE, auditd, aggiornamenti di sicurezza automatici, Monit con avvisi via email (spazio, servizi, **ultimo backup ricevuto** da ciascun server).
7. **Nessun servizio web** nella prima versione: meno superficie di attacco.

## Alternative considerate

- **NAS Synology con Borg da SynoCommunity o in container:** dipende da pacchetti di terze parti e dal sistema del produttore; non riproducibile con Ansible.
- **Proxmox Backup Server:** ottimo per gli snapshot delle VM, ma non per i backup applicativi di EduWISP; resta un complemento consigliato (ADR-0016).
- **restic con rest-server in modalità append-only:** valido e libero; Borg resta preferito per coerenza con l'ADR-0016.
- **Archivio su cloud:** possibile solo con fornitori nell'UE e accordi ex art. 28 GDPR; rinviato al pilota.

## Conseguenze

- Il ruolo `ansible-eduwisp` deve poter inviare i backup a un archivio remoto via SSH (issue #6), con una chiave dedicata per server.
- L'archivio attuale sulla VM del server va sostituito da uno nuovo con chiave e passphrase nuove.
- La ISO del server di backup si aggiunge al lavoro della ISO principale, alla fine.
- Ambiente di prova: `backup.eduwisp.org`, VM su Proxmox con un disco dati da 100 GB.
