---
title: "ADR-0018: Interfaccia per ruoli e accesso delle famiglie"
parent: Decisioni (ADR)
nav_order: 18
---

# ADR-0018: Interfaccia per ruoli e accesso delle famiglie

- **Stato:** Accettata
- **Data:** 2026-11-27 (punto 5 aggiornato lo stesso giorno)

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

5. **Studenti maggiorenni:** con la maggiore età la responsabilità genitoriale cessa (art. 2 c.c.) e lo studente decide da sé sui propri dati.
   - **Per impostazione predefinita i familiari perdono l'accesso** dal giorno in cui lo studente diventa maggiorenne.
   - Lo studente può **decidere dal proprio tablet** se lasciare l'accesso ai familiari, e cambiare idea in qualsiasi momento. Finché non sceglie, l'accesso resta chiuso.
   - La scelta si conferma con il **blocco schermo del tablet** (PIN, sequenza o impronta), così non la può fare un'altra persona che ha il tablet in mano.
   - La scelta vale per tutti i familiari collegati ed è **registrata** nel registro delle operazioni.
   - La scuola registra la **data di nascita** dello studente: l'età è di ciascuno, non della classe (chi ripete l'anno può essere più grande dei compagni). Se ne ricavano solo le soglie di legge, 18 anni e 14 anni del consenso digitale (vedi il [quadro normativo](../sicurezza-privacy/quadro-normativo.md#età-dei-minori)). *Modifica del 28 novembre 2026: prima si registrava solo la data della maggiore età, che contiene la stessa informazione ma non permette la soglia dei 14 anni.*
   - Ai familiari senza accesso il portale mostra solo che lo studente è maggiorenne e che i dati sono visibili con il suo consenso.

6. **Selettore di vista per l'amministratore** («vedi come»):
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
- Nuovo repository **`eduwisp-portal`** per l'interfaccia per ruoli: pagine di dirigente, docente e famiglia, area «Amministrazione della piattaforma» e «vedi come».
- `eduwisp-audit` riceve il primo codice: registro in sola aggiunta, usato dal «vedi come» e dagli accessi fuori ambito.
- Protocollo v0: la policy indica al tablet se chiedere la scelta allo studente; il rapporto di stato riporta la scelta (campi facoltativi, compatibili con gli agenti esistenti).
- Il «vedi come» è attivo anche nell'ambiente demo, dove l'amministratore può vedere la piattaforma come dirigente, docente o famiglia del liceo di esempio.
- `eduwisp-school`: modello del collegamento famiglia-studente (tipo di relazione, referente, attivo) e interrogazione `students_for_guardian`, con il limite di due collegamenti attivi e un solo referente per studente.
- Dati della demo: famiglie inventate, con casi di uno e due genitori, tutori e fratelli.
- Il Family Control ([ADR-0014](0014-family-control-facoltativo-multipiattaforma.md)) userà lo stesso collegamento; chi tra i due può attivarlo va definito nel modulo.
- L'accesso con SPID o CIE per le famiglie (ADR-0013) resta da valutare.
