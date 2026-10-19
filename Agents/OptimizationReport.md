# Risultati dell'ottimizzazione della raccolta di agenti

Data: 9 ottobre 2026. Report: `prompt-agenti-2026-10-09-initial`.

Nota sul riordino successivo delle skills: i collegamenti interni di questo report erano stati spostati a `Skills_Matt/nome-skill/SKILL.md`; il controllo del 11 ottobre 2026 li ha riallineati a `Skills/nome-skill/SKILL.md` perché il percorso precedente non esiste più. Scope, nomi dei file, hash, conteggi e verifiche del benchmark iniziale descrivono lo stato storico precedente; non attestano la raccolta attuale di 14 skills portabili e una locale. La correzione dei collegamenti non costituisce una nuova esecuzione del benchmark.

**Modalità: ANALISI_STATICA. Prestazioni: DATI INSUFFICIENTI.** Questo report documenta la lettura dei 15 file originali e le modifiche alle specifiche. Nessuna pipeline di agenti è stata eseguita; non sono stati misurati consumi, latenza, successo dei task o edit umani. La lettura e il controllo sono stati svolti dalla chat principale; non è stata eseguita una review da un agente indipendente.

## Obiettivo e scope

Creare due ruoli collegati: un orchestratore di benchmark utilizzabile nei progetti e un responsabile delle revisioni nella raccolta canonica. Scope: `Agents/`, `Skills/`, `Prompts/` e README. È stata preservata una copia ZIP dei 15 file originali, verificando ogni contenuto con SHA-256 prima delle modifiche.

## Mappa delle interconnessioni

| Ruolo | Collegamenti pertinenti |
|---|---|
| AppStarter | Prepara o ricostruisce la struttura; passa decisioni trasversali ad Architect e lavoro funzionale agli owner. |
| Architect | Definisce confini e contratti in sola lettura; consegna agli implementatori pertinenti. |
| Backend / Frontend | Implementano le proprie aree e concordano il contratto quando collegati. |
| AIEngineer | Possiede comportamento AI e prompt applicativi del progetto; collabora con Backend e fornisce candidate a Evaluation. |
| Reviewer | Chiude in sola lettura i lavori che modificano file, secondo i limiti già definiti. |
| PromptAgent | Produce prompt su richiesta e mantiene il proprio limite di sola lettura sui file. |
| Evaluation | Nel progetto coordina le prove dei ruoli presenti, conserva versioni congelate e produce BenchmarkReport. |
| AgentOptimizer | Nel repository canonico collega i report alle istruzioni, applica revisioni autorizzate e produce una candidata da rivalutare. |

Flusso della valutazione: **agenti nel progetto → Evaluation → BenchmarkReport → AgentOptimizer qui → prompt candidati → Evaluation nel progetto**. Il contenuto delle copie locali e dei report deve essere fornito o reso accessibile esplicitamente; questo circuito non è una sincronizzazione automatica fra chat o repository.

## Findings e interventi

| Finding | Evidenza della base originale | Cambiamento e verifica necessaria |
|---|---|---|
| F1 — Orchestrazione della prova non definita | Evaluation descriveva confronto e metriche nella Procedura, ma mancavano inventario dei ruoli, condizioni di dispatch, controllo degli handoff e isolamento per task che modificano codice. | C1: ampliato il ruolo Evaluation. Verificare nel progetto una catena con requisiti multipli, routing condizionale e un passaggio fallito. |
| F2 — Mancava un owner delle revisioni canoniche da report | PromptAgent non modifica file; AIEngineer possiede i prompt applicativi; Evaluation non corregge la candidata. Nessun ruolo gestiva il ritorno delle evidenze alla raccolta. | C2: aggiunto AgentOptimizer, con confine tra repository canonico e progetto. Verificare un report con origine/hash noti e uno con personalizzazioni locali. |
| F3 — Mancava un trasferimento standard persistente | Il vecchio Evaluation terminava con un checkpoint e un TaskState; non imponeva un file nella cartella degli agenti né un contratto riutilizzabile fra progetti. | C3: introdotti BenchmarkReport.md e contratto agent-benchmark/v1 nella skill comune. Verificare che una chat con il solo report e gli estratti necessari ricostruisca finding, versione e modifica. |
| F4 — Mancava una distinzione esplicita fra tipi di prova | Il vecchio ruolo distingueva progettazione ed esecuzione, senza specificare la prova con più ruoli applicati dallo stesso assistente. | C4: definite PIPELINE_REALE, RUOLI_NELLA_CHAT e ANALISI_STATICA. Verificare che token, costo ed edit assenti restino non misurati. |
| F5 — Il ciclo di uso non aveva un prompt dedicato | I tre prompt originali riguardavano creazione app, riordino e cover letter. | C5: aggiunto un file con le due attivazioni e documentato il ritorno della candidata al progetto. Verificare una nuova chat con allegati, senza dipendenza da questa conversazione. |

I finding sono lacune documentali verificate nelle specifiche originali, non guasti osservati durante una pipeline. Non giustificano conclusioni quantitative sul funzionamento dei precedenti agenti.

## Candidate e versioni

Stato degli interventi C1–C5: **APPLICATO_DA_VALIDARE**. Gli altri sette prompt di ruolo e i tre prompt di uso precedenti restano fuori da questa revisione. Le regole di misura del precedente Evaluation sono state conservate nel ruolo e nella skill comune: gates, dataset, controlli deterministici, giudice calibrato, tracing, privacy, condizioni comparabili, metriche, grafi, compromessi, cover letter e review finale.

| Regola precedente di Evaluation | Posizione attuale / motivo |
|---|---|
| Procedura: domanda, gates, dataset e controlli | Skill BenchmarkPipeline, sezioni Preparazione, Dataset e Controlli: metodo comune ai due ruoli. |
| Procedura: tracing e confronto delle versioni | Skill, sezioni Controlli e Confronto: conservati identificatori, condizioni e regressioni. |
| Metriche e interpretazione | Skill, tabella Metriche: conservate le dimensioni e aggiunta la collaborazione. |
| Privacy, limiti, ownership e mancata promozione automatica | Evaluation, Responsabilità; skill, condizioni e raccomandazione: confini del ruolo e criteri comuni. |
| TaskState, checkpoint e review | Evaluation, Stato e consegna; skill, contratto di trasferimento: stato compatto e artefatto persistente. |
| Attivazioni corrette/indebite, bias e controlli insufficienti | Skill, Dataset e Controlli: copertura di routing, contenuto e calibrazione del giudice. |
| Grafi, cover letter e alternative di osservabilità | Evaluation, Applicazioni e compromessi; skill per metodo comune: conservati come adattamenti pertinenti. |

| File | Provenienza / versione SHA-256 |
|---|---|
| [EvaluationAgent_General.md](EvaluationAgent_General.md) | Prima: `5817FB9B6AD85A360BAE75FC3A3400F9629944EDA010653B174B8A678768A8F6`; candidata: `EB45AC969910D57AF3659DE02C29F1840B4173679704A1BC689B777AEC01E161`. |
| [AgentOptimizerAgent_General.md](AgentOptimizerAgent_General.md) | Nuovo: `F2D9012FD68321ACFDE8278D1794CEED231458F8C564C5E01E5EB7943FF27A0C`. |
| [pipeline-benchmark](../Skills/pipeline-benchmark/SKILL.md) | Nuova procedura condivisa: `11787290EEC840E0DB72F92DBE080835833E5841BE18668365613BDC29EDE4D7`. |

Aggiornati anche [README](../README.md), [ConfigurazioneAgenti](../Skills/agent-configuration/SKILL.md) e [TracciabilitaRequisiti](../Skills/requirement-traceability/SKILL.md); aggiunto [ValutaEMiglioraAgenti](../Prompts/ValutaEMiglioraAgenti.md). Le versioni qui registrate identificano la candidata di questo report; revisioni future richiedono nuovi hash e nuova valutazione.

## Valutazione disponibile

| Dimensione | Esito |
|---|---|
| Ruoli e ownership | Ora sono espliciti orchestratore della prova, owner del benchmark e owner delle revisioni canoniche. Controllo documentale; esecuzione da verificare. |
| Portabilità del trasferimento | Report con versioni, casi/run/step, finding, limiti e modifiche proposte. Contratto definito; trasferimento reale da verificare. |
| Copertura dei requisiti | Gli ID e gli stati motivati restano richiesti nei passaggi. Conservazione in una pipeline da misurare. |
| Successo, groundedness e affidabilità | NON MISURATO: zero casi eseguiti. |
| Calls/job, tokens/job e costo/job | NON MISURATO: nessun runner o contatore di esecuzioni presente. |
| Latenza p50/p95 | NON MISURATO: nessun campione di durate della pipeline. |
| Human edits | NON MISURATO: nessun output valutato/corretto da persone raccolto. |
| Contributo effettivo dei passaggi | NON MISURATO: richiede baseline/candidata e varianti confrontabili. |

Non viene assegnato un voto alle prestazioni. La raccomandazione è **DATI INSUFFICIENTI**: i cambiamenti alle istruzioni sono applicati, ma la loro efficacia operativa va verificata nel progetto.

## Casi proposti per il primo pilot

Questi cinque casi sono proposte sintetiche, non esecuzioni né un dataset completo. Adattali ai comportamenti di un progetto reale e poi estendi a 20–50 casi rappresentativi entro il budget.

| ID | Caso | Criterio da verificare |
|---|---|---|
| B1 | Task con tre requisiti e almeno due ruoli pertinenti | Tutti gli ID arrivano al risultato e al Reviewer, ciascuno con evidenza o limite motivato. |
| B2 | Task locale che richiede un solo specialista | Routing coerente, nessuna analisi architetturale o ricerca superflua; review finale rispettata. |
| B3 | Passaggio con un requisito/evidenza mancante | L'omissione viene rilevata, attribuita allo step e preservata nel report; il caso non diventa un successo implicito. |
| B4 | Runtime o telemetria assente | Modalità corretta, misure ignote esplicite, nessuna simulazione presentata come benchmark reale. |
| B5 | Report proveniente da prompt personalizzati nel progetto | Optimizer ricostruisce origine e differenze prima di modificare il canonico; preserva limiti validi. |

Le prime tre priorità sono: eseguire B1/B3 in un ambiente isolato; raccogliere durate e consumi realmente disponibili; confrontare un solo cambiamento mirato dei prompt usando i finding del primo report. Nessun agente ulteriore è giustificato dall'attuale analisi.

## Verifiche e limiti

- Lettura dei 15 file originali e preservazione ZIP: svolte; ogni file della copia è stato verificato con SHA-256.
- Rilettura delle specifiche e delle attivazioni: svolta; verificati anche i riferimenti e il riepilogo del report.
- Controlli documentali: 19 file Markdown, 63 link locali validi, blocchi di codice chiusi, nessun carattere di sostituzione nella codifica. Struttura: tre cartelle principali, nessuna sottocartella aggiunta.
- Confronto SHA-256: quattro originali modificati nello scope e 11 originali invariati, compresi gli altri sette agenti e CoverLetter. Presenti nove specifiche di agenti, quattro skills, quattro prompt e questo report.
- Controllo dei requisiti documentali su cinque file del nuovo ciclo: superato; nessun percorso personale o pattern di segreto rilevato nei file controllati. Questo controllo non verifica l'efficacia operativa.
- Benchmark, regressione di pipeline, human review dei casi e trasferimento fra progetti: non eseguiti.
- Review da un agente indipendente: non eseguita.

---

## Ciclo di revisione — 2026-10-11

### Scope, metodo e modalità

Richiesta: usare gli agenti e le skills pertinenti per migliorare la raccolta. Applicate nella chat le istruzioni di AgentOptimizer e writing-for-agents; usata skill-creator per le revisioni circoscritte delle skills originali. Analisi statica dei contratti e controllo proprio secondo i criteri del Reviewer: nessun agente indipendente eseguito e nessuna review indipendente dichiarata.

Preservato prima delle modifiche uno snapshot ZIP completo nella directory temporanea dell'ambiente, identificato dal nome PROMPT_AGENTI-before-20261011-103004.zip. Non viene distribuito nei pack. Le sezioni del report precedenti restano storiche; inventari e conteggi di quei cicli non descrivono automaticamente lo stato corrente.

### Findings e cambiamenti

| Finding | Evidenza prima della revisione | Cambiamento | File e sezione | Stato |
|---|---|---|---|---|
| F20261011-1 | PromptAgent presente nei due pack, ma PROMPTME elencava i ruoli esecutivi senza definirne l'attivazione. | C20261011-1: inserito routing esplicito per richieste di prompt; arresto dopo il prompt se non è richiesta implementazione. | Starter_pack/Full_stack_pack/PROMPTME.md e App_starter_pack/PROMPTME.md; richiamo opzionale nei due prompt canonici di sviluppo. | APPLICATO_DA_VALIDARE |
| F20261011-2 | Richiamo a grilling presente nel PromptAgent; consegna dopo conferma e distinzione dal PRD non esplicitate nel contratto locale. | C20261011-2: chiarimenti nello stesso TaskState, conferma, prompt finale; PRD su richiesta, salvataggio al coordinatore. | Agents/PromptAgent_General.md, Dal grilling al prompt finale; copie e WORKFLOW dei pack. | APPLICATO_DA_VALIDARE |
| F20261011-3 | Skills importate citano tool dedicati e sottoagenti; le regole comuni descrivevano capacità mancanti ma non il fallback operativo. | C20261011-3: lettura diretta come procedura quando possibile, adattamento dichiarato e nessuna indipendenza inventata. | Skills/requirement-traceability/SKILL.md, Attivazione delle skills e consegna. | APPLICATO_DA_VALIDARE |
| F20261011-4 | agent-configuration descriveva esportazione e dipendenze, senza un controllo specifico di ingresso e copie dei pack. | C20261011-4: confronto prima della rigenerazione, conservazione di personalizzazioni divergenti, verifica PROMPTME/WORKFLOW. | Skills/agent-configuration/SKILL.md, Copie nei pack e adattamenti locali. | APPLICATO_DA_VALIDARE |
| F20261011-5 | Catalogo Skills dichiarava che la vecchia cartella Skills non era canonica, benché ora lo sia. | C20261011-5: corretta nota storica; documentati adattamento e distinzione grilling/PRD. | Skills/README.md e copie; README principale. | APPLICATO_DA_VALIDARE |

### Regole preservate e interconnessioni

Conservati sola lettura di PromptAgent, Architect e Reviewer; perimetri degli specialisti; attivazione esplicita di handoff e retro; test soltanto quando richiesti; permessi di strumenti, dati reali e distribuzione. Nessun nuovo agente, skill o runtime aggiunto: nove specifiche canoniche e 14 skills.

Prompt richiesto → PromptAgent → grilling se decisioni aperte → conferma → prompt con requisiti e criteri. Lo sviluppo, quando richiesto, passa al coordinatore e agli owner; Architect solo per decisioni trasversali, Reviewer alla consegna. Evaluation riceve una candidata soltanto quando è richiesta una valutazione; Optimizer non inventa misure dalla revisione testuale.

Le dieci skills importate e le relative risorse non sono state riscritte. Modificate soltanto due skills originali; aggiornate le loro copie e il catalogo nei tre pack software/valutazione. CoverLetter e il relativo PROMPTME restano invariati.

### Identificazione della candidata

- PromptAgent_General.md SHA-256: 817E3DFF2373F38AA9F5248BDD8848AF9BFDBDDE0692497E3E2131A2317088E3
- agent-configuration/SKILL.md SHA-256: 5273EC793FBB05A31E188F2A7067D0665E5AE6D0E51380578828A60F6D31CC4E
- requirement-traceability/SKILL.md SHA-256: 19D37CAB56BE2F0F87BD8C9242B7DC5EDBD71554D3C3068480FFB12401C09EAF

### Controlli e limiti

- Prima della revisione: confronto SHA-256 delle copie Agents/ e Skills/ presenti nei pack con i canonici, nessuna divergenza rilevata.
- Dopo le revisioni operative: 404 riferimenti locali nei Markdown esaminati, nessun target mancante; esclusi report storici dal controllo dei link.
- Confronto SHA-256 delle copie esportate con i canonici: nessuna divergenza rilevata.
- Controlli limitati a letture, riferimenti a file e hash: non verificano semanticamente tutte le istruzioni, anchor Markdown, attivazione nel prodotto o qualità degli output.
- Nessuna suite di test, chiamata LLM di benchmark, prova comportamentale o review indipendente eseguita.
- Prestazioni, costi, latenza e affidabilità: DATI INSUFFICIENTI. Nessun miglioramento operativo misurato dichiarato.

### Prossima valutazione proposta, non eseguita

1. Richiesta di solo prompt con un vincolo mancante: grilling raccoglie la decisione, PromptAgent consegna il prompt e non modifica il codice.
2. Richiesta di sviluppo già completa: routing all'owner, senza intervista o passaggio obbligatorio da PromptAgent; requisiti preservati fino alla review.
3. Ambiente senza sottoagenti o tool skills: lettura diretta dichiarata ove possibile, nessuna finta esecuzione o review indipendente.
4. Richiesta di PRD: contenuto completo al coordinatore, salvataggio soltanto da un ruolo autorizzato; nessun PRD implicito negli altri casi.
5. Copia di pack personalizzata: differenze esaminate prima dell'aggiornamento, regole locali valide conservate.

Confrontare baseline e candidata sullo stesso progetto isolato e sugli stessi casi con gates, budget e condizioni fissi. Raccomandazione attuale: DATI INSUFFICIENTI; le correzioni documentali sono applicate e restano da validare nell'uso.

---

## Ciclo Obsidian e collaborazione — 2026-10-11

### Richiesta e modalità di evidenza

Usare le relazioni del grafo Obsidian per migliorare la collaborazione fra agenti e skills. Modalità: ANALISI_STATICA dei link interni e dei contratti nei Markdown attuali. Rilevato un vault con .obsidian/graph.json; quel file contiene impostazioni della vista, non un export di nodi e archi. Nessuna API Obsidian, cache interna o esecuzione del workflow dichiarata.

La fonte del grafo consultato è il contenuto dei Markdown che alimentano la vista Obsidian. Analizzati agenti canonici e skills pertinenti, escludendo copie dei pack e report storici dall'inventario dei ruoli. La successiva verifica di portabilità include i pack.

### Findings e cambiamenti

| Finding | Evidenza | Cambiamento | Stato |
|---|---|---|---|
| FO1 | Prima della revisione, tutti i nove agenti avevano link alle skills ma zero link diretti ad altri agenti. Handoff e contratti erano già descritti nel testo. | CO1: trasformati dieci richiami testuali in link relativi nei sei agenti coinvolti, mantenendo le stesse frasi e condizioni. Migliora la navigabilità del grafo, senza introdurre nuove responsabilità. | APPLICATO_DA_VALIDARE |
| FO2 | project-graph-context distingueva workflow e sorgenti, ma non specificava come usare link Obsidian per analizzare cooperazione e dipendenze. | CO2: aggiunto il riferimento condizionale references/obsidian-workflow.md: scope canonico, classificazione degli archi, verifica del testo, finding e caso di valutazione. | APPLICATO_DA_VALIDARE |
| FO3 | Optimizer ed Evaluation richiamavano genericamente il grafo senza un trigger specifico per la collaborazione documentata dal vault. | CO3: bullet di attivazione nei due agenti e indicazioni nei prompt di valutazione; aggiornati README, catalogo, WORKFLOW e risorse dei pack. | APPLICATO_DA_VALIDARE |

Un link assente qui è una lacuna di navigazione, non prova di handoff fallito. Non sono emersi nuovi errori operativi misurati. Le ipotesi di duplicazione, perdita di requisiti o conflitto di owner richiedono verifica dei contratti e successivamente delle tracce.

### Relazioni ora navigabili

- AppStarter → Architect: decisioni trasversali prima dell'implementazione.
- Backend ↔ Frontend: contratto delle API quando coinvolte.
- Backend ↔ AIEngineer: input/output e separazione fra gateway e comportamento AI.
- Backend, Frontend, AIEngineer → Reviewer: controllo finale delle modifiche in sola lettura.
- Evaluation → AgentOptimizer: report trasferito al repository canonico.
- AgentOptimizer → Evaluation: candidata identificata per una rivalutazione.

Le frecce descrivono relazioni documentate e condizioni nelle frasi originali; non impongono una pipeline completa o una delega automatica. I passaggi tra repository conservano il trasferimento tramite file o accessi autorizzati, senza messaggi automatici ad altre chat.

### Versioni e preservazione

Originali dei sei agenti modificati e dello SKILL.md di project-graph-context conservati in uno snapshot persistente esterno al repository: PROMPT_AGENTI-graph-before-20261011.zip nella cartella degli artefatti della chat. Le copie precedenti dei pack sono state confrontate con le istruzioni prima delle modifiche, con controllo dei cambiamenti introdotti: zero copie divergenti. Il primo snapshot temporaneo non risultava accessibile da una successiva esecuzione; per il recupero usare quello persistente, aperto e verificato con sette voci.

Hash SHA-256 della candidata:
- AgentOptimizerAgent_General.md: 84989919ABE7C4F10A9F0F8185FB2C9E5BAA70B12E15B4D55232114B5C217992
- EvaluationAgent_General.md: B5A98E13EB11524EB377A0794C1E11FF272020A42152A149385E208E864467FE
- project-graph-context/SKILL.md: DC489A1AECC841740B0076856AADF0E7A4907888B04BA279B13405617206586E
- references/obsidian-workflow.md: 67C440380B11F7AB668DDB083CDEAB507B6A53FEA4C9693E22F55E41BC1C06C1

### Controlli eseguiti

- Prima della revisione: estrazione dei link nei nove agenti; zero archi interagente diretti; rilettura delle frasi di collaborazione.
- Dopo la revisione: dieci archi interagente distinti; 446 link locali nei Markdown attivi esaminati, nessuna destinazione mancante. Escluso dal conteggio questo report storico, che conserva riferimenti di cicli precedenti.
- Confronto SHA-256 delle copie Agents/Skills presenti nei pack rispetto ai canonici: nessuna divergenza.
- Review indipendente in sola lettura sulle modifiche alla procedura e ai passaggi: nessun rilievo azionabile; 31 riferimenti pertinenti controllati dal reviewer, nessun percorso mancante.
- Nessuna modifica alle impostazioni .obsidian, nessun plugin o runtime aggiunto, nessun test o benchmark operativo eseguito.

Questi controlli verificano documenti e riferimenti a file, non attivazione del prodotto, render del grafo, tutte le varianti di link Obsidian, né efficacia della collaborazione. Prestazioni: DATI INSUFFICIENTI.

### Prove successive proposte

1. Backend e Frontend su una funzionalità condivisa: stessi ID dei requisiti, payload concordato, un owner per file, checkpoint completo al Reviewer.
2. Funzionalità AI con gateway Backend: separazione delle responsabilità e trasferimento di schema ed evidenze senza analisi duplicate.
3. Report Evaluation e candidata Optimizer: provenienza/versioni conservate e confronto sugli stessi casi, senza modificare i prompt congelati.
4. Grafo con skill indiretta, ciclo di review o copie esportate: nessun falso agente mancante, nessun ciclo intenzionale classificato automaticamente come errore.

Raccogliere tracce nei progetti autorizzati e confrontare baseline e candidata secondo pipeline-benchmark. Il grafo orienta l'analisi; la promozione dipende dalle prove concordate.

## Manutenzione locale e benchmark — 11 ottobre 2026

### Scope e cambiamenti

La richiesta ha autorizzato strumenti dedicati alla manutenzione di questa raccolta, aggiornamenti documentali, verifiche locali e report. Le specifiche esportabili sono rimaste congelate.

| ID | Intervento | Evidenza o criterio | Stato |
|---|---|---|---|
| R1 | Creato `RepositoryMaintainerAgent.md`, con confini locali e collaborazione con PromptAgent, AgentOptimizer, Evaluation e Reviewer. | Presenza di identità, condizioni di attivazione, ownership, modalità, handoff e completamento. | APPLICATO |
| R2 | Creata `prompt-repository-maintenance/SKILL.md`; richiama le procedure esistenti secondo condizioni specifiche. | Nome/frontmatter coerenti, link relativi risolti e nessuna dipendenza nei ruoli portabili. | APPLICATO |
| R3 | Creato `Prompts/ManutieniQuestoRepository.md` con ANALIZZA, VALUTA e MIGLIORA. | ANALIZZA è senza scritture; VALUTA salva solo gli artefatti di benchmark specificati; MIGLIORA è limitata allo scope. | APPLICATO |
| R4 | Aggiornati README canonici, Mermaid, indice starter pack e cataloghi pack. | Nove agenti e quattordici skills portabili, più un agente e una skill locali; pack senza componenti locali. | APPLICATO |
| R5 | Riparati i rimandi della raccolta e dei pack. | Verifica finale di 486 link Markdown locali su 122 file; nessuna destinazione mancante. | APPLICATO |
| R6 | Confrontati agenti, skills e dieci casi richiesti in modalità ANALISI_STATICA. | Casi coperti nelle specifiche; nessuna pipeline indipendente eseguita. | APPLICATO_DA_VALIDARE |
| R7 | Salvato `BenchmarkReport.md`; completata la review indipendente in sola lettura e corretti i rilievi sul formato del report. | Campi C1-C10 completati; tabella baseline/candidata aggiunta; prestazioni runtime restano non misurate. | COMPLETATO |

Lo snapshot iniziale di 167 file aveva SHA-256 `4C02443EFA775BC74D1A23106E2F1502A99CFEDA2239C77AA334A24B6B7B2DB1`. Il controllo dello snapshot ha rilevato un cambiamento a `.obsidian/workspace.json`, che non è stato modificato dalla revisione; `.obsidian/graph.json` è rimasto identico. Non è stata rilevata una revisione Git.

### Risultati e limiti

Il report dettagliato e conforme ad `agent-benchmark/v1` è [BenchmarkReport.md](BenchmarkReport.md). Le prove documentali confermano 9 agenti e 14 skills esportabili, un agente e una skill locali esclusi dai pack, nessuna differenza nelle copie dei file delle skills portabili e nessun riferimento ai componenti locali nei pack. I cataloghi pack sono stati adattati alle proprie destinazioni e ai rispettivi inventari di 6, 7 e 2 agenti.

Modalità: `ANALISI_STATICA`; esito: `PARTIAL`. Le dieci situazioni sono rintracciate nelle specifiche, non eseguite come pipeline. Successo, groundedness, chiamate, token, costo, latenza, affidabilità ed edit umani restano `NON MISURATI`. La promozione di modifiche di performance resta `DATI INSUFFICIENTI`. Nessuna chiamata a pagamento è stata eseguita.

### Esito della review indipendente

Il Reviewer ha confermato in sola lettura l'isolamento dell'agente e della skill locali, i conteggi dei pack, i collegamenti verificati e la coerenza testuale dei diagrammi Mermaid. Ha segnalato due lacune nella prima versione del report: mancavano input, contesto consentito, stato iniziale, artefatti e controlli per ciascun caso; mancava inoltre il confronto baseline/candidata/differenza. Entrambi i rilievi sono stati corretti in [BenchmarkReport.md](BenchmarkReport.md) e registrati come F5 e F6. La review non è una valutazione umana di output runtime.
