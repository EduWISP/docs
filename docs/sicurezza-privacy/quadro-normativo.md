---
title: Quadro normativo
parent: Sicurezza e privacy
nav_order: 3
---

# Quadro normativo

EduWISP tratta dati di **minori** in un contesto **scolastico**, spesso per conto di **pubbliche amministrazioni**. Il rispetto della normativa italiana ed europea è un **vincolo bloccante** del progetto, non un requisito negoziabile (vedi [ADR-0008](../decisioni/0008-conformita-normativa.md)).

{: .important }
> Questa pagina è un elenco di lavoro per la progettazione, **non è consulenza legale**. Ogni riferimento va verificato sui testi vigenti ([Normattiva](https://www.normattiva.it/), [EUR-Lex](https://eur-lex.europa.eu/), [Garante Privacy](https://www.garanteprivacy.it/)) e validato con il DPO dell'istituto e con consulenti qualificati prima di trattare dati reali. Le voci contrassegnate con *da verificare* richiedono un approfondimento specifico.

## Protezione dei dati personali

| Norma | Cosa comporta per EduWISP |
|---|---|
| **Reg. (UE) 2016/679 (GDPR)** — art. 5 | Principi di liceità, minimizzazione, limitazione della finalità e della conservazione, integrità e riservatezza, responsabilizzazione. |
| GDPR — art. 6 e 9 | Per le scuole statali la base giuridica tipica è l'esecuzione di un compito di interesse pubblico o un obbligo di legge, non il consenso. I dati delle segnalazioni di cyberbullismo possono rientrare nelle categorie particolari (art. 9) o comunque essere dati delicati: serve un'analisi caso per caso. |
| GDPR — art. 8 e considerando 38 | I minori meritano una protezione specifica. In Italia, per i servizi della società dell'informazione, l'età del consenso digitale è **14 anni** (art. 2-quinquies Codice privacy). |
| GDPR — art. 12-14 | Informative chiare e **comprensibili per un minore**, oltre che per le famiglie. |
| GDPR — art. 22 | Nessuna decisione basata unicamente su trattamento automatizzato con effetti significativi sugli studenti. |
| GDPR — art. 25 | Privacy by design e by default: le impostazioni predefinite devono essere le più protettive. |
| GDPR — art. 28 | Chi ospita o gestisce EduWISP per conto della scuola è **responsabile del trattamento**: serve un contratto (o altro atto giuridico) con i contenuti previsti. |
| GDPR — art. 30 | Il progetto deve fornire alle scuole le informazioni per il **registro dei trattamenti**. |
| GDPR — art. 32 | Misure di sicurezza adeguate al rischio (cifratura, controllo accessi, resilienza, test periodici). |
| GDPR — art. 33-34 | Gestione delle violazioni: notifica al Garante entro 72 ore quando dovuta, comunicazione agli interessati se il rischio è elevato. |
| GDPR — art. 35 | **DPIA** probabilmente necessaria: dati di minori (soggetti vulnerabili), monitoraggio dei dispositivi, segnalazioni di cyberbullismo. |
| GDPR — art. 37-39 | Le scuole pubbliche hanno un **DPO** obbligatorio: va coinvolto fin dalla progettazione. |
| GDPR — art. 44 e seguenti | Trasferimenti extra-UE solo con garanzie adeguate. Obiettivo del progetto: **dati in UE**. Da valutare con attenzione i flussi verso i servizi Google (Android Management API). |
| **D.Lgs. 196/2003 (Codice privacy)**, come modificato dal D.Lgs. 101/2018 | Art. 2-ter (base giuridica per i trattamenti pubblici), 2-quinquies (consenso del minore), 2-sexies (dati particolari per motivi di interesse pubblico rilevante). |
| **Provvedimenti e indicazioni del Garante** | Vademecum per le scuole (*«La scuola a prova di privacy»*) e provvedimenti su registro elettronico, pubblicazione dei dati, videosorveglianza. *Da verificare: edizione vigente e provvedimenti specifici applicabili.* |

## Minori e cyberbullismo

| Norma | Cosa comporta per EduWISP |
|---|---|
| **Convenzione ONU sui diritti dell'infanzia** (ratificata con L. 176/1991) | Il **superiore interesse del minore** guida ogni scelta progettuale; diritto alla riservatezza (art. 16). |
| **L. 71/2017** sul cyberbullismo, modificata dalla **L. 70/2024** | Ruolo del **referente scolastico** per il bullismo e il cyberbullismo, obblighi di informazione delle famiglie, procedure di segnalazione. Il modulo [Cyberbullismo](../moduli/cyberbullismo.md) deve supportare queste procedure senza sostituirle. *Da verificare: obblighi introdotti dalla L. 70/2024 e decreti attuativi.* |
| **Linee di orientamento MIM** per la prevenzione e il contrasto di bullismo e cyberbullismo | Indicazioni operative per le scuole (protocolli, team antibullismo). *Da verificare: versione vigente.* |

## Età dei minori

L'età di ogni studente si calcola dalla **data di nascita**, mai dalla classe: chi ripete un anno può essere più grande dei compagni. *Verifica del 28 novembre 2026.*

| Età | Norma | Cosa comporta per EduWISP |
|---|---|---|
| **14 anni** | Art. 2-quinquies del Codice privacy (D.Lgs. 101/2018), in deroga all'art. 8 del GDPR | Da 14 anni il minore può acconsentire da sé ai servizi della società dell'informazione; sotto i 14 serve chi esercita la responsabilità genitoriale. Le informative per i minori devono essere chiare e adatte all'età. |
| **14 anni** | L. 132/2025 sull'intelligenza artificiale, art. 4 c. 4 (in vigore dal 10 ottobre 2025) | Sotto i 14 anni l'accesso a sistemi di IA richiede il consenso dei genitori; dai 14 anni il minore può acconsentire se le informazioni sono comprensibili. |
| **14 anni** | L. 71/2017 sul cyberbullismo | Il minore ultraquattordicenne può chiedere da sé l'oscuramento o la rimozione dei contenuti. |
| **16 anni** | GDPR, art. 8 | Soglia predefinita del consenso digitale negli Stati che non l'hanno abbassata (minimo 13). In Italia vale 14: per installazioni in altri Stati la soglia è configurabile (`EDUWISP_DIGITAL_CONSENT_AGE`). |
| **18 anni** | Art. 2 c.c. | Con la maggiore età la responsabilità genitoriale cessa: in EduWISP i familiari perdono l'accesso, salvo consenso dello studente dal tablet ([ADR-0018](../decisioni/0018-interfaccia-per-ruoli.md)). |

**Proposte non ancora legge** (da seguire): emendamenti e disegni di legge sull'accesso dei minori ai social (divieto sotto i 13 anni, account collegato a quello dei genitori fino a 15 o 16 anni). Non cambiano EduWISP, dove i social sono già vietati sui tablet degli studenti ([ADR-0019](../decisioni/0019-app-consentite.md)), ma vanno verificati se approvati.

## Intelligenza artificiale

| Norma | Cosa comporta per EduWISP |
|---|---|
| **Reg. (UE) 2024/1689 (AI Act)** — art. 5 | **Vietato** il riconoscimento delle emozioni nei contesti educativi (salvo eccezioni mediche o di sicurezza). |
| AI Act — allegato III, punto 3 | Sono **ad alto rischio** i sistemi di IA in ambito di istruzione, tra cui quelli che monitorano comportamenti vietati degli studenti durante le prove: rilevante per la "modalità verifica" e per qualsiasi analisi assistita delle segnalazioni. |
| **L. 132/2025** (legge italiana sull'IA) | Disposizioni specifiche per i minori, tra cui il consenso dei genitori per l'accesso dei minori di 14 anni a tecnologie di IA. *Da verificare: articoli applicabili.* |

**Posizione del progetto:** nessuna funzione di IA è prevista nel perimetro iniziale. Qualsiasi proposta futura richiede un ADR dedicato, l'analisi AI Act e una DPIA.

## Lavoratori (docenti e personale)

| Norma | Cosa comporta per EduWISP |
|---|---|
| **L. 300/1970 (Statuto dei lavoratori)**, art. 4 | I log e gli audit sulle azioni dei docenti e del personale possono costituire controllo a distanza: limiti, informativa e, dove richiesto, procedure sindacali. |
| Codice privacy, art. 113-114 | Trattamento dei dati nel rapporto di lavoro e garanzie sul controllo a distanza. |

## Pubblica amministrazione

| Norma | Cosa comporta per EduWISP |
|---|---|
| **D.Lgs. 82/2005 (CAD)**, art. 68-69, e **Linee guida AgID** su acquisizione e riuso del software | Le PA devono valutare software open source e a riuso: EduWISP dovrebbe essere idoneo al catalogo di Developers Italia. |
| **L. 4/2004 (Legge Stanca)** e Linee guida AgID sull'accessibilità | Le interfacce usate dalle scuole devono essere accessibili (riferimento tecnico EN 301 549 / WCAG). Collegato a RNF-008. |
| **Qualificazione dei servizi cloud per la PA (ACN)** | Un'offerta *cloud hosted* destinata alle scuole statali deve rispettare i requisiti di qualificazione ACN. *Da verificare: livello richiesto per i dati trattati.* |

## Indicazioni del Garante per le scuole

Fonti: le [FAQ «Scuola e privacy»](https://www.gpdp.it/home/faq/scuola-e-privacy) e il vademecum [«La scuola a prova di privacy»](https://www.gpdp.it/scuola) (edizione 2023, presentato anche da [AID](https://www.aiditalia.org/news/la-scuola-a-prova-di-privacy-le-indicazioni-del-garante-della-privacy)). Le indicazioni che riguardano EduWISP:

| Indicazione del Garante | Conseguenza per EduWISP |
|---|---|
| I dati su disabilità, DSA e salute li conoscono solo i soggetti legittimati (docenti, genitori, operatori del PEI) e non si diffondono (FAQ 6 e 8) | Nessuna diagnosi né motivo sanitario nei dati della piattaforma; le eccezioni per uno studente (per esempio app del PDP) non riportano il motivo e sono visibili solo a chi lo segue |
| Gli studenti con DSA possono usare gli strumenti previsti dal PDP, compresi registratore e computer, anche se il regolamento vieta le registrazioni (FAQ 12) | L'elenco di app consentite deve permettere app **per il singolo studente** (registratore, sintesi vocale, mappe concettuali), decise dalla scuola |
| Nelle comunicazioni non rivolte a destinatari precisi non compaiono alunni identificabili: disabilità, salute, bullismo, sanzioni (FAQ 6 e 7) | Notifiche e richieste (per esempio di app) vanno **solo** ai destinatari interessati, mai in elenchi o bacheche generali |
| L'uso dello smartphone lo disciplina la scuola; registrazioni e foto solo per uso personale, la diffusione richiede il consenso (FAQ 9, 10, 11) | Fotocamera e registrazione restano impostazioni della scuola; nessuna raccolta di foto o registrazioni da parte di EduWISP |
| La scuola è titolare e deve dare l'informativa, anche online (FAQ 1 e 2) | EduWISP fornirà un modello di informativa e il fornitore del servizio agisce come responsabile del trattamento (art. 28 GDPR) |
| Videosorveglianza solo se strettamente indispensabile (FAQ 14) | EduWISP non usa fotocamera, microfono o schermo dei tablet per sorvegliare |

## Regole che ne derivano per il progetto

1. **Nessun dato reale** di studenti, famiglie o personale prima di DPIA, revisione legale e approvazione del DPO.
2. **Minimizzazione:** ogni dato raccolto deve avere una finalità documentata, una base giuridica e un tempo di conservazione.
3. **Nessuna profilazione** degli studenti, nessuna classifica, nessun punteggio comportamentale.
4. **Nessuna decisione automatizzata** con effetti sugli studenti; supervisione umana sempre.
5. **Nessuna sorveglianza occulta**: niente lettura di messaggi, keylogging, cattura dello schermo nascosta, geolocalizzazione continua.
6. **Trasparenza verso il minore**: lo studente deve poter vedere, in linguaggio adatto all'età, quali regole sono attive e quali dati vengono trattati.
7. **Dati nell'Unione europea**, con flussi verso terze parti mappati e documentati.
8. **Supporto agli adempimenti della scuola**: modelli per registro dei trattamenti, informative, DPIA e nomina del responsabile.
