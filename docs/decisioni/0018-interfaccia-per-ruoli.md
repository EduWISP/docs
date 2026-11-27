---
title: "ADR-0018: Interfaccia per ruoli e accesso delle famiglie"
parent: Decisioni (ADR)
nav_order: 18
---

# ADR-0018: Interfaccia per ruoli e accesso delle famiglie

- **Stato:** Proposta (punti 1–5 decisi; punto 6 in attesa di conferma)
- **Data:** 2026-11-27

## Contesto

L'interfaccia web di EduWISP serve persone con compiti molto diversi. Mostrare a tutti le stesse pagine, filtrando solo i menu, non basta: con dati di minori la separazione degli accessi è un obbligo di **minimizzazione e protezione fin dalla progettazione** (GDPR art. 5 e 25, [ADR-0008](0008-conformita-normativa.md)).

Per le famiglie bisogna tenere conto che:

- la responsabilità genitoriale è esercitata **da entrambi i genitori** (art. 316 c.c.), anche dopo la separazione (art. 337-ter c.c.); la scuola deve garantire a entrambi l'accesso alle informazioni sul figlio (nota MIUR 5336 del 2 settembre 2015);
- ci sono però molti casi con **un solo genitore** o con un **tutore** (art. 343 e seguenti c.c.) o un affidatario;
- un provvedimento del giudice può **limitare** la responsabilità di un genitore;
- una famiglia può avere **più figli** nello stesso istituto.

## Decisione

1. **Quattro aree di accesso**, ciascuna con il proprio menu e le proprie pagine:

   | Area | Ruolo (`Role`) | Vede |
   |---|---|---|
   | Amministratore di sistema | account di piattaforma (`is_superuser`), non legato a un istituto | **tutto, in tutti gli istituti**, e le impostazioni che nessun altro ruolo vede |
   | Amministratore IT dell'istituto | `it_admin` | dispositivi, applicazioni e policy del proprio istituto |
   | Dirigente (preside) | `school_admin` | tutto il proprio istituto |
   | Docente | `teacher` | solo le classi dei propri incarichi nell'anno in corso (`classes_for_teacher`, RF-010) |
   | Famiglia | `guardian` | solo i propri figli (`students_for_guardian`) |

2. **Amministratore di sistema.** È l'unico che vede e imposta tutto:
   - **istituti** (organizzazioni): crearli, configurarli, disattivarli; plessi, indirizzi e sezioni di ciascuno;
   - **utenti e ruoli** di ogni istituto, compresi dirigenti e amministratori IT;
   - **impostazioni della piattaforma**: posta, autenticazione, conservazione dei dati, integrazioni, aggiornamenti;
   - dispositivi, applicazioni e policy di tutti gli istituti;
   - il selettore di vista (punto 6).

   Queste pagine non compaiono e non sono raggiungibili per gli altri ruoli. Gli accessi dell'amministratore ai dati personali sono **registrati** e non modificabili da lui stesso (GDPR art. 32; provvedimento del Garante sugli amministratori di sistema del 27 novembre 2008). Gli account di amministratore sono pochi, nominativi e con **autenticazione a più fattori** obbligatoria.

3. **I permessi si controllano sul server**, in ogni vista e in ogni API, a partire dagli insiemi della tabella; l'interfaccia nasconde solo ciò che il server comunque rifiuterebbe. Un tentativo di accesso fuori ambito risponde 404 e viene registrato.

4. **Famiglia: un referente obbligatorio, un secondo facoltativo.** Per ogni studente la scuola collega **almeno una** persona con responsabilità (genitore, tutore o affidatario) e **al massimo due** con accesso.
   - Le due persone hanno **gli stessi diritti di consultazione**. «Referente» indica solo chi riceve per primo le comunicazioni: non esiste un «capofamiglia» che escluda l'altro.
   - Il secondo si aggiunge quando lo chiede: per esempio un genitore separato. La scuola verifica la relazione (RF-020) prima di attivare l'accesso.
   - Se un provvedimento del giudice limita un genitore, la scuola **disattiva** il suo collegamento. Si registra solo che è disattivato e quando, non il contenuto del provvedimento.
   - Lo stesso account vale per **tutti i figli** nell'istituto.
   - L'accesso termina quando lo studente lascia l'istituto.

5. **Studenti maggiorenni:** il comportamento predefinito (accesso delle famiglie mantenuto, sospeso o soggetto al consenso dello studente) va definito con il DPO prima del pilota. Fino ad allora il sistema non fa ipotesi e lascia la scelta all'istituto.

6. **Selettore di vista per l'amministratore** («vedi come»), *proposta in attesa di conferma*:
   - un menu a tendina permette all'amministratore di vedere l'interfaccia **come** il dirigente, un docente o una famiglia;
   - **sola lettura**: nessuna azione è possibile mentre è attivo;
   - un **avviso sempre visibile** in alto indica il ruolo e la persona simulati, con il pulsante per uscire;
   - ogni attivazione è **registrata** nel registro degli accessi (chi, come chi, quando, per quanto);
   - sui **dati reali** va indicato un **motivo** (per esempio la richiesta di assistenza); nell'ambiente demo non serve.

## Alternative considerate

- **Un solo «capofamiglia» per studente:** più semplice, ma escluderebbe l'altro genitore, che ha diritto alle informazioni. Scartata.
- **Nessun limite al numero di persone collegate:** aumenta i dati trattati e il rischio di accessi impropri (per esempio nuovi partner senza responsabilità genitoriale). Scartata.
- **Impersonazione completa** (l'amministratore agisce come l'utente): permetterebbe azioni a nome di altri. Scartata a favore della sola lettura.

## Conseguenze

- `eduwisp-users`: nuovo ruolo `guardian` («genitore o tutore»); l'amministratore di sistema è un account di piattaforma, senza appartenenza a un istituto.
- Interfaccia: un'area «Amministrazione della piattaforma» separata, per istituti e impostazioni.
- `eduwisp-school`: modello del collegamento famiglia-studente (tipo di relazione, referente, attivo) e interrogazione `students_for_guardian`, con il limite di due collegamenti attivi e un solo referente per studente.
- Dati della demo: famiglie inventate, con casi di uno e due genitori, tutori e fratelli.
- Il Family Control ([ADR-0014](0014-family-control-facoltativo-multipiattaforma.md)) userà lo stesso collegamento; chi tra i due può attivarlo va definito nel modulo.
- L'accesso con SPID o CIE per le famiglie (ADR-0013) resta da valutare.
