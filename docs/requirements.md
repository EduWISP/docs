# Requisiti

I requisiti seguenti sono una baseline progettuale da discutere e validare. Non costituiscono una dichiarazione di funzionalità già implementate.

## Requisiti funzionali

### Organizzazioni e identità
- RF-001: supportare più istituti con separazione logica dei dati.
- RF-002: gestire ruoli e permessi granulari.
- RF-003: rappresentare plessi, classi, gruppi, docenti e studenti.
- RF-004: associare e riassegnare dispositivi secondo procedure autorizzate.

### MDM e applicazioni
- RF-010: registrare dispositivi tramite procedure di provisioning supportate.
- RF-011: mantenere inventario minimo di dispositivo e software.
- RF-012: assegnare app obbligatorie e facoltative.
- RF-013: applicare configurazioni gestite e restrizioni compatibili.
- RF-014: supportare profili didattici e modalità temporanee, se consentite dal provider.
- RF-015: registrare esito e data di sincronizzazione delle policy.

### Family Control
- RF-020: verificare l'associazione genitore/tutore-studente.
- RF-021: permettere regole familiari aggiuntive negli ambiti autorizzati.
- RF-022: rendere visibili le regole attive e la loro provenienza.
- RF-023: impedire che una regola familiare annulli una baseline di sicurezza.

### Cyberbullismo e benessere
- RF-030: offrire un canale di segnalazione semplice e accessibile.
- RF-031: consentire segnalazioni da parte di ruoli autorizzati.
- RF-032: gestire presa in carico, assegnazione, stato e follow-up.
- RF-033: limitare l'accesso ai casi secondo necessità e ruolo.
- RF-034: conservare un audit delle consultazioni e delle modifiche.
- RF-035: fornire contenuti educativi e risorse di prevenzione.

## Requisiti non funzionali

- RNF-001: privacy by design e minimizzazione dei dati.
- RNF-002: isolamento tra tenant.
- RNF-003: autenticazione robusta e autorizzazioni verificabili.
- RNF-004: comunicazioni cifrate.
- RNF-005: audit non alterabile dagli utenti ordinari.
- RNF-006: supporto a cloud hosting e self-hosting.
- RNF-007: documentazione delle API e dei limiti del provider.
- RNF-008: accessibilità e usabilità per studenti e personale.
- RNF-009: funzionamento resiliente in caso di connettività intermittente, nei limiti del sistema Android.
- RNF-010: procedure di backup, ripristino e gestione degli incidenti da specificare.

## Criteri di accettazione progettuale

Prima dello sviluppo ogni requisito dovrà avere: identificativo, motivazione, stakeholder, priorità, dipendenze, rischi, criteri verificabili e stato (proposto/approvato/respinto).
