# Audit statico del routing delle skills

**Data:** 13 ottobre 2026  
**Modalità:** sola lettura; è stato creato soltanto questo report, come consentito dalla richiesta. Nessun agente, skill, prompt o pack è stato modificato.

## Esito sintetico

Le nove specifiche canoniche degli agenti portabili hanno una sezione esplicita **Skills per il task** e rimandano a skills canoniche con condizioni per fase o situazione. La selezione evita di imporre tutte le skills a ogni richiesta. Le quattordici skills portabili risultano raggiungibili direttamente o tramite un router documentato: `handoff`, per esempio, si attiva solo su richiesta di una nuova sessione attraverso `requirement-traceability`.

Ho rilevato due correzioni utili alla precisione del routing, una lacuna di documentazione del catalogo e un’istruzione poco chiara nei README di due starter pack. Non ho trovato link Markdown rotti o differenze nei contenuti canonici delle copie incluse nei pack. L’analisi misura copertura documentale: non dimostra la qualità operativa degli agenti e non misura task success, token, costi o latenza.

## Skills locali applicate

| Procedura | Percorso | Uso nell’audit | Risultato |
|---|---|---|---|
| `prompt-repository-maintenance` | `.codex/skills/prompt-repository-maintenance/SKILL.md` | Ha definito confini tra laboratorio locale, prodotti canonici, pack e report. | I ruoli `.codex/` sono stati distinti dagli agenti esportabili; i report storici sono esclusi dall’inventario degli agenti. |
| `agent-graph-analysis` | `.codex/skills/agent-graph-analysis/SKILL.md` e `Skills/project-graph-context/references/obsidian-workflow.md` | Ho ricostruito link Markdown e letto le frasi che stabiliscono condizioni, ownership e destinatari. | Catene e contratti sono stati controllati nelle fonti; il grafo è trattato come navigazione documentale, non come prova di esecuzione. |
| `static-agent-evaluation` | `.codex/skills/static-agent-evaluation/SKILL.md` | Ho confrontato responsabilità, input/output, attivazione, dipendenze e consegne delle specifiche. | Esiti classificati come coperti, lacune o non verificabili, con findings circoscritti. |
| `export-pack-validation` | `.codex/skills/export-pack-validation/SKILL.md` | Ho controllato contenuto, dipendenze e isolamento delle copie nei quattro pack. | I contenuti degli agenti e delle skills inclusi nei pack corrispondono alle fonti canoniche. |
| `agent-design` | `.codex/skills/agent-design/SKILL.md` | Ho formulato le correzioni mantenendo ruolo, trigger, input/output e permessi. | Le proposte indicano il punto preciso, il testo da inserire e il motivo, senza applicarle. |
| `scope-and-handoff` | `.codex/skills/scope-and-handoff/SKILL.md` | Ho verificato requisiti, owner e condizioni di consegna locale. | Non essendoci stata delega, non è stato preparato un handoff a una nuova sessione. |

`grilling` non è stato attivato: l’inventario e i confini del task erano specificati e non è emersa una decisione sostanziale necessaria per completare l’audit.

I quattro TOML locali (`lab_prompt_agent`, `lab_agent_designer`, `lab_static_evaluator`, `lab_repository_reviewer`) sono presenti nel repository, ma in questa sessione l’inventario dei ruoli chiamabili ha restituito soltanto `/root`. Quindi il valutatore e il reviewer locali non sono stati eseguiti come ruoli indipendenti: la chat principale ha applicato le loro procedure statiche, senza simulare una delega o una review indipendente.

## A. Inventario

| Area | Contenuto effettivo | Interpretazione |
|---|---|---|
| `.codex/agents/` | 4 configurazioni TOML: PromptAgent, AgentDesigner, StaticEvaluator, RepositoryReviewer. | Ruoli locali del laboratorio; non sono prodotti generali da esportare. |
| `.codex/skills/` | 7 procedure locali: `agent-design`, `agent-graph-analysis`, `export-pack-validation`, `grilling`, `prompt-repository-maintenance`, `scope-and-handoff`, `static-agent-evaluation`. | Supporto alla manutenzione di questo repository. |
| `Agents/` | 9 specifiche canoniche: PromptAgent, AppStarter, Architect, Backend, Frontend, AIEngineer, Reviewer, Evaluation, AgentOptimizer; inoltre `BenchmarkReport.md`, `OptimizationReport.md` e `StaticEvaluation.md`. | I tre report non sono agenti né nuove fonti canoniche. |
| `Skills/` | 14 skills canoniche: `agent-configuration`, `requirement-traceability`, `project-graph-context`, `pipeline-benchmark`, `grilling`, `handoff`, `writing-for-agents`, `codebase-design`, `diagnosing-bugs`, `retro`, `investigate-first`, `surgical-patch`, `safe-refactor`, `verify-and-stop`. | Procedure portabili; ogni skill mantiene la propria cartella e il suo `SKILL.md`. |
| `Prompts/` | `CoverLetter.md`, `CreaAppDaZero.md`, `RiorganizzaAppEsistente.md`, `ValutaEMiglioraAgenti.md`. | Punti di ingresso e prompt da incollare, non specifiche di ruolo. |
| `Starter_pack/` | `Cover_letter_Pack`, `Full_stack_pack`, `App_starter_pack`, `Evaluation_pack`. | Copie distribuibili con istruzioni di attivazione; non fonti canoniche. Cover Letter è un processo autonomo e non copia agenti/skills canonici. |

I pack includono rispettivamente 7 agenti in App Starter, 6 in Full Stack e 2 in Evaluation; i pack di sviluppo contengono anche le 14 skills portabili. `Cover_letter_Pack` contiene un `PROMPTME.md` autonomo, senza agenti o skills copiati. La composizione risulta coerente con i rispettivi scopi dichiarati.

## B. Matrice agente–skill

In tabella, la colonna **Input → output** riassume il contratto della skill. `Diretto` indica un richiamo nella specifica dell’agente; `Instradato` indica una dipendenza/condizione esplicita in una skill comune o nel catalogo. Le attivazioni restano condizionali: la presenza di una skill non impone l’intera procedura in ogni task.

| Agente/i | Skill | Attivazione | Input → output atteso | Fonte canonica | Esito statico |
|---|---|---|---|---|---|
| Tutti i 9 ruoli portabili | `agent-configuration` | Creare o aggiornare istruzioni del ruolo, non eseguire un task ordinario. | Specifica, ambiente e istruzioni esistenti → istruzioni portabili o differenze motivate, dipendenze e limiti. | `Skills/agent-configuration/SKILL.md` | Diretto e appropriato; manca il rinvio specialistico a `writing-for-agents` durante la stesura (F2). |
| Tutti i 9 ruoli portabili | `requirement-traceability` | Task articolato, multi-area o con passaggi tra ruoli; per un task semplice, checklist breve. | Richiesta, scope, fonti e stato → R-ID, criteri, owner, dipendenze, prove e stati conservati nel TaskState. | `Skills/requirement-traceability/SKILL.md` | Diretto; l’attivazione e la selezione delle altre skills sono definite chiaramente. |
| Tutti i 9 ruoli portabili | `project-graph-context` | Quando link, dipendenze o impatto trasversale sono utili. | Markdown/grafo e fonti → archi pertinenti, condizioni, owner e limiti verificati nei file. | `Skills/project-graph-context/SKILL.md` | Diretto e condizionale; nessun arco è trattato da solo come prova di collaborazione osservata. |
| Evaluation; AgentOptimizer; AIEngineer; Reviewer | `pipeline-benchmark` | Evaluation misura e confronta; AIEngineer prepara baseline/candidata/rubrica quando cambia una pipeline; AgentOptimizer formula candidata e prova successiva; Reviewer esamina un benchmark incluso nella consegna. | Casi, prompt/versioni, rubriche, trace e risultati disponibili → confronto strutturato, report o finding limitati alle prove. | `Skills/pipeline-benchmark/SKILL.md` | Diretto e coerente nei prompt; il catalogo incompleto nomina solo Evaluation e AgentOptimizer (F4). |
| PromptAgent; AppStarter; Architect; AIEngineer; Evaluation; AgentOptimizer | `grilling` | Quando manca una decisione sostanziale su obiettivo, vincoli, priorità, gates o budget; non per requisiti già chiari. | Richiesta e decisioni aperte → domande a tappe, requisiti confermati e punti ancora aperti. | `Skills/grilling/SKILL.md` | Diretto e condizionale; non genera automaticamente un PRD. |
| Tutti i ruoli, tramite il router comune; consegna esplicita su nuova sessione | `handoff` | Solo quando l’utente chiede di preparare una nuova sessione; i passaggi ordinari restano nel TaskState. L’invocazione è esplicita (`disable-model-invocation: true`). | Conversazione, stato e artefatti esistenti → documento temporaneo conciso, riferimenti e skills suggerite. | `Skills/handoff/SKILL.md`; `Skills/requirement-traceability/SKILL.md` | Instradato correttamente; non è una skill orfana e non impone handoff per ogni consegna. La portabilità dipende dalla possibilità di leggere/invocare il file nell’ambiente di destinazione. |
| PromptAgent; AIEngineer; AgentOptimizer; Reviewer | `writing-for-agents` | Scrittura/revisione di prompt, skills o istruzioni consumate da agenti. | Testo e comportamento richiesto → trigger, puntatori, gerarchia, criteri e contenuti più precisi senza duplicazioni. | `Skills/writing-for-agents/SKILL.md` e, per creare una skill, `SKILL-MECHANICS.md` | Diretto in questi ruoli. La skill è pertinente anche alla fase di scrittura di `agent-configuration`, che oggi non la richiama (F2). |
| AppStarter; Architect; Backend; Frontend; AIEngineer; Reviewer | `codebase-design` | Confini, interfacce, dipendenze o testabilità da progettare/valutare; Architect e Reviewer restano in sola lettura. | Requisiti e struttura reale → contratti e confini proporzionati, alternative e limiti. | `Skills/codebase-design/SKILL.md` | Diretto; responsabilità e permessi restano rispettati. |
| Backend; Frontend; AIEngineer | `diagnosing-bugs` | Bug difficile, intermittente o non spiegato dopo aver riusato le prove di `investigate-first`. | Sintomo, contesto e prove → riproduzione/diagnosi verificabile e fix circoscritto proposto. | `Skills/diagnosing-bugs/SKILL.md` | Diretto e condizionale. I test richiesti dalla procedura restano soggetti a permessi e autorizzazione via `requirement-traceability`. |
| AppStarter; Backend; Frontend; AIEngineer; Evaluation | `investigate-first` | Causa incerta nell’area posseduta; Evaluation la usa per guasti del proprio runner/raccolta. | Sintomo, codice/runner e prove → causa o ipotesi distinta dai fatti, con prossima verifica mirata. | `Skills/investigate-first/SKILL.md` | Diretto e limitato all’ownership; nessuna sovrapposizione obbligatoria con diagnosi avanzata. |
| AgentOptimizer; coordinatore | `retro` | Su richiesta di retrospettiva della sessione, non automaticamente. | Sessione e artefatti autorizzati → proposte per l’ambiente, trasferite come ipotesi all’Optimizer. | `Skills/retro/SKILL.md` | Instradato tramite `requirement-traceability` e descritto nel catalogo; attivazione su richiesta coerente. |
| Backend; Frontend; AIEngineer; Evaluation (sola strumentazione propria); Reviewer (solo criteri in lettura) | `surgical-patch` | Correzione localizzata del difetto nell’area posseduta; per Evaluation solo strumentazione propria. | Difetto e prove → modifica minima o criteri di correzione/review; verifica secondo permessi. | `Skills/surgical-patch/SKILL.md` | Diretto; Reviewer non scrive e Evaluation non modifica prompt/prodotto altrui. |
| AppStarter; Backend; Frontend; AIEngineer; Architect (piano); Reviewer (criteri) | `safe-refactor` | Riordino richiesto; Architect pianifica e Reviewer valuta in sola lettura. Non sostituisce un fix funzionale. | Baseline, mappa delle dipendenze e struttura → piano/modifica reversibile, compatibilità e verifiche proporzionate. | `Skills/safe-refactor/SKILL.md` | Diretto; ownership e sola lettura sono dichiarate. |
| Tutti i ruoli nei rispettivi limiti | `verify-and-stop` | Verifica richiesta o criterio di completamento assegnato; Reviewer controlla solo prove leggibili. | Criteri, artefatti e prove consentite → esito per criterio, limiti e condizione di arresto. | `Skills/verify-and-stop/SKILL.md` | Diretto; non attribuisce capacità o permessi mancanti. |

### Copertura esplicita per agente

- **PromptAgent:** `requirement-traceability`, `writing-for-agents`, `grilling` su decisioni aperte, `project-graph-context` quando utile. Produce prompt, non esegue il task.
- **AppStarter:** `agent-configuration`, `requirement-traceability`, `grilling`, `codebase-design`, `safe-refactor`, `investigate-first`, `verify-and-stop`, `project-graph-context`.
- **Architect:** `agent-configuration`, `requirement-traceability`, `grilling`, `codebase-design`, `safe-refactor` per pianificare, `project-graph-context`; non applica modifiche.
- **Backend:** `agent-configuration`, `requirement-traceability`, `codebase-design`, `investigate-first` o `diagnosing-bugs`, `surgical-patch`, `safe-refactor`, `verify-and-stop`, `project-graph-context`.
- **Frontend:** stessi trigger di sviluppo del Backend, con ownership UI e integrazione API: `agent-configuration`, `requirement-traceability`, `codebase-design`, `investigate-first` o `diagnosing-bugs`, `surgical-patch`, `safe-refactor`, `verify-and-stop`, `project-graph-context`.
- **AIEngineer:** `agent-configuration`, `requirement-traceability`, `writing-for-agents`, `grilling`, `codebase-design`, `investigate-first` o `diagnosing-bugs`, `surgical-patch`, `safe-refactor`, `verify-and-stop`, `pipeline-benchmark` per preparare il passaggio, `project-graph-context`.
- **Evaluation:** `agent-configuration`, `pipeline-benchmark`, `requirement-traceability`, `project-graph-context`, `grilling`, `investigate-first` e `surgical-patch` solo per il runner proprio, `verify-and-stop`.
- **AgentOptimizer:** `agent-configuration`, `pipeline-benchmark`, `requirement-traceability`, `project-graph-context`, `writing-for-agents`, `grilling` sui conflitti, `retro` su richiesta, `verify-and-stop`.
- **Reviewer:** `agent-configuration`, `project-graph-context`, `requirement-traceability`, `verify-and-stop`, `codebase-design`, `writing-for-agents`, `surgical-patch` e `safe-refactor` come criteri, `pipeline-benchmark` se la consegna contiene un benchmark. Rimane in sola lettura.

## C. Difetti e D. Modifiche proposte

Le proposte seguenti sono testi da applicare se si autorizza una fase di correzione; durante questo audit non sono state applicate.

### F1 — Il PromptAgent locale non richiama la skill di progettazione

**Gravità: media.** In `.codex/agents/prompt-agent.toml`, sezione `developer_instructions` (secondo paragrafo, riga 7), il ruolo prepara prompt per creare o migliorare agenti e skills. Richiama grilling e analisi del grafo, ma non la procedura locale `agent-design`, che esplicita i campi che il prompt di un agente/skill deve coprire e il confine PromptAgent → Designer.

**Testo esatto proposto**, da aggiungere dopo la frase che richiama `grilling` e `agent-graph-analysis`:

> Se la richiesta riguarda la creazione o revisione delle istruzioni di un agente o di una skill, applica `.codex/skills/agent-design/SKILL.md` per ruolo, trigger, input/output, responsabilità, permessi, dipendenze, collaborazione e completamento; per un prompt operativo non applicarla.

**Motivo:** rende il metodo di progettazione raggiungibile quando serve, senza caricare la procedura per ogni prompt ordinario e senza consentire al PromptAgent di modificare file.

### F2 — La configurazione non instrada alla procedura specializzata di scrittura

**Gravità: media.** `Skills/agent-configuration/SKILL.md`, passo 4, richiede di preparare istruzioni portabili ma non collega `writing-for-agents`. I ruoli che non hanno un richiamo diretto alla skill di scrittura possono quindi creare/aggiornare prompt senza il metodo dedicato a trigger, puntatori, gerarchia informativa, criteri e potatura. Un richiamo nella procedura canonica risolve la lacuna senza duplicarlo in ogni agente.

**Testo esatto proposto**, da aggiungere alla fine del passo 4:

```md
Quando prepari o modifichi il testo delle istruzioni, applica anche [writing-for-agents](../../Skills/writing-for-agents/SKILL.md) per trigger, puntatori, criteri di completamento e potatura; se stai creando una skill, leggi anche il relativo `SKILL-MECHANICS.md`.
```

**Motivo:** il trigger è la fase di stesura, non ogni task svolto dall’agente; il riferimento a `SKILL-MECHANICS.md` resta limitato alla creazione di una skill.

### F3 — I README dei pack sviluppo menzionano un ruolo non incluso

**Gravità: bassa.** `Starter_pack/App_starter_pack/README.md:17` e `Starter_pack/Full_stack_pack/README.md:17` dicono “Per Evaluation scegli…” ma questi pack non includono l’agente Evaluation; esso è nel pack dedicato. L’istruzione può far pensare che il prompt Evaluation sia dentro il pack corrente.

**Testo esatto proposto**, per sostituire il punto 5 in entrambi i README:

```md
5. Evaluation non è incluso in questo pack. Per un benchmark nel progetto o per migliorare i prompt nel repository canonico, usa [Evaluation_pack](../../Starter_pack/Evaluation_pack/README.md) e scegli il `PROMPTME.md` della fase richiesta.
```

**Motivo:** chiarisce dove reperire il ruolo e conserva la distinzione tra benchmark sul progetto e miglioramento delle specifiche canoniche.

### F4 — Il catalogo delle skills sottostima gli utilizzatori del benchmark

**Gravità: bassa.** `Skills/README.md:41` elenca solo Evaluation e AgentOptimizer per `pipeline-benchmark`; le specifiche AIEngineer e Reviewer la richiamano direttamente per la preparazione di un confronto e la review di un benchmark. Il README principale già descrive queste due funzioni, quindi è una discrepanza del catalogo.

**Testo esatto proposto**, in sostituzione della riga del catalogo:

```md
| [pipeline-benchmark](../../Skills/pipeline-benchmark/SKILL.md) | Preparare casi ripetibili, misure e confronti di pipeline. | Evaluation (esecuzione e misure), AIEngineer (prepara la consegna per il confronto), AgentOptimizer (candidate e prova successiva), Reviewer (controlla gli artefatti del benchmark in sola lettura). |
```

**Motivo:** documenta i diversi livelli di uso senza attribuire a AIEngineer o Reviewer l’esecuzione e le misure che competono a Evaluation.

## E. Skills senza utilizzatori

Non ho trovato skills portabili completamente prive di un utilizzatore o di un router documentato.

- `handoff` non ha un link diretto dalle nove specifiche, ma `requirement-traceability` la instrada quando l’utente chiede il passaggio a una nuova sessione; README e descrizione della skill riportano il vincolo di invocazione esplicita. È un uso intenzionale, non un orfano.
- `retro` si attiva su richiesta ed è attribuita ad AgentOptimizer/coordinatore.
- `writing-for-agents` è esplicitamente collegata ai ruoli che producono o revisionano prompt; la mancanza nel percorso canonico `agent-configuration` è trattata in F2.
- `pipeline-benchmark` è usata da più ruoli, ma il catalogo non li elenca tutti: F4.
- `scope-and-handoff` è una skill locale, elencata e richiamata dalla procedura comune `prompt-repository-maintenance` e da AgentDesigner. Gli altri ruoli locali sono guidati dalla procedura comune e dai contratti di consegna nel TOML/README; non propongo di aggiungere richiami ripetuti senza un caso concreto che dimostri una perdita di requisiti.

## Grafo e separazione

Il controllo ha trovato **488 link Markdown relativi, 0 wikilink e 0 link relativi non risolti**. Il collegamento Mermaid nel README descrive sia le responsabilità nel lavoro sul codice sia il ciclo Evaluation → `BenchmarkReport.md` → AgentOptimizer → candidata → nuova valutazione. Le frasi collegate chiariscono che: AppStarter passa ad Architect per confini e decisioni trasversali; Backend e Frontend concordano contratti condivisi; AIEngineer collabora con Backend quando l’AI attraversa il gateway server; gli owner consegnano ID e prove al Reviewer; Evaluation misura nel progetto e AgentOptimizer modifica le specifiche nel repository canonico. Il ciclo di review è limitato a correzione mirata e nuovo controllo.

I link sono relazioni documentate, non prova che gli agenti siano stati eseguiti in quella sequenza. Non ho aperto Obsidian né verificato la resa visuale; `.obsidian/graph.json` è configurazione della vista, mentre i Markdown forniscono gli archi. I file del grafo locale e dei prodotti restano distinti; i pack non richiamano `.codex/`, `AGENTS.md` locale o ruoli `lab_*`.

## Controlli eseguiti e limiti

- Inventariati agenti, skills, prompt, pack, report e configurazioni locali dai file effettivi.
- Letti integralmente i nove file canonici degli agenti e i quattordici `SKILL.md` portabili; approfondite le risorse richiamate per i casi pertinenti.
- Controllate le condizioni di attivazione, input/output, limiti, destinatari, handoff ordinari e richiesta di handoff a nuova sessione.
- Il controllo iniziale aveva contato 488 link Markdown relativi. Una verifica successiva ha individuato tre percorsi non risolti in questo stesso report storico; sono stati corretti. Il controllo aggiornato dell’intero repository è registrato in [SkillRoutingRuntimeInstallAudit](SkillRoutingRuntimeInstallAudit.md).
- Confrontati i contenuti copiati nei pack: 0 differenze nei file degli agenti e nei contenuti delle skills; presenti le istruzioni `PROMPTME.md` e `WORKFLOW.md` per i pack in cui il processo li prevede. Cover Letter rimane un flusso standalone.
- `git status` non è disponibile: nella cartella corrente non è presente `.git` e Git restituisce “not a git repository”. In questo turno ho scritto soltanto questo report, ma non posso attestare lo stato preesistente o altri cambiamenti non tracciati.
- Nessun test o pipeline è stato eseguito. Non sono state raccolte trace né misure di task success, groundedness operativa, calls/job, tokens/job, costo, latenza p50/p95, affidabilità o interventi umani.
- I quattro ruoli TOML locali sono configurati nei file ma non erano disponibili come sottoagenti chiamabili in questa sessione; valutazione e review indipendenti sono quindi **non eseguite**. La chat principale ha applicato le procedure richieste in modo statico.
- La qualità dell’integrazione runtime, il caricamento delle skills nell’ambiente di destinazione e la capacità di conservare davvero i requisiti nelle conversazioni restano da verificare con casi osservati.

