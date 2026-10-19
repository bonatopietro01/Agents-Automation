# Audit del routing e dell'installazione runtime nei pack

**Data:** 13 ottobre 2026  
**Modalità:** analisi statica, documentazione runtime aggiornata e correzioni circoscritte ai prompt/readme.  
**Destinazione software:** non fornita in questa sessione; non è stato installato alcun agente o skill in un'app esterna.

## Esito

Le nove specifiche canoniche portabili hanno una sezione esplicita `Skills per il task`; le condizioni e i limiti sono coperti nel routing seguente. Ho applicato i quattro rilievi del precedente [SkillRoutingAudit.md](SkillRoutingAudit.md), aggiunto nei tre pack software/valutazione istruzioni per installare adattamenti locali al progetto, e rimosso riferimenti dal catalogo portabile al laboratorio locale. Le fonti canoniche restano in `Agents/` e `Skills/`; i pack contengono copie derivate.

La nuova installazione configurata da PROMPTME riguarda l'assistente di coding che lavora sul repository. Non aggiunge agenti alla logica eseguita dall'applicazione. Il prompt crea le cartelle mancanti soltanto nel repository di destinazione, dopo averne rilevato il runtime e controllato i file esistenti. La verifica di riconoscimento runtime resta a carico della chat che opererà sul progetto.

## Procedure locali applicate

| Skill | Percorso | Applicazione e risultato |
|---|---|---|
| `prompt-repository-maintenance` | `.codex/skills/prompt-repository-maintenance/SKILL.md` | Ha mantenuto distinti laboratorio locale, fonti portabili, prompt, report e copie dei pack. |
| `agent-graph-analysis` | `.codex/skills/agent-graph-analysis/SKILL.md` e `Skills/project-graph-context/references/obsidian-workflow.md` | Ho seguito link Markdown e verificato condizioni, input/output, ownership e destinatari nelle specifiche. Il grafo resta supporto di navigazione, non prova di esecuzione. |
| `static-agent-evaluation` | `.codex/skills/static-agent-evaluation/SKILL.md` | Ho confrontato trigger, permessi, handoff, dipendenze e skills dei nove agenti. |
| `export-pack-validation` | `.codex/skills/export-pack-validation/SKILL.md` | Ho confrontato fonti e copie, segnalando e correggendo link portabili e copie specifiche del pack. |
| `agent-design` | `.codex/skills/agent-design/SKILL.md` | Ho mantenuto i ruoli esistenti e aggiunto agli adattatori runtime il contratto di routing concreto delle skills. |

I quattro TOML locali sono fonti del laboratorio, ma i ruoli non erano invocabili come subagenti in questa sessione. La chat principale ha applicato le procedure richieste senza simulare esecuzione o review indipendente. `scope-and-handoff` non è stato applicato a un handoff perché non ho delegato il lavoro. Grilling non era necessario: per i formati Codex/Claude le fonti ufficiali e il prompt allegato determinavano le scelte; per altri runtime i PROMPTME richiedono la documentazione ufficiale rilevata.

## A. Inventario effettivo

| Area | Contenuto | Ruolo nel sistema |
|---|---|---|
| `.codex/agents/` | 4 configurazioni TOML: PromptAgent, AgentDesigner, StaticEvaluator, RepositoryReviewer. | Ruoli del laboratorio locale, non esportati. |
| `.codex/skills/` | 7 procedure di manutenzione e valutazione locali. | Metodi per aggiornare questa raccolta. |
| `Agents/` | 9 specifiche canoniche: PromptAgent, AppStarter, Architect, Backend, Frontend, AIEngineer, Reviewer, Evaluation, AgentOptimizer; inoltre 3 report storici. | I report non sono agenti né fonti canoniche. |
| `Skills/` | 14 skills canoniche. | Procedure portabili, ciascuna con cartella e `SKILL.md`. |
| `Prompts/` | 4 prompt di ingresso: cover letter, app da zero, riorganizzazione app esistente, valutazione/miglioramento agenti. | Istruzioni di avvio, non ruoli. |
| `Starter_pack/` | Cover Letter, Full Stack, App Starter ed Evaluation. | Copie distribuibili con `PROMPTME.md`; i pack software includono anche `WORKFLOW.md`, agenti e skills. |

Composizione dei ruoli nei pack: App Starter 7 agenti, Full Stack 6, Evaluation 2 specifiche. Per il benchmark di un progetto si installa il solo Evaluation; AgentOptimizer serve al repository canonico e non va installato nel software valutato. Cover Letter è un processo autonomo, senza agenti/skills di coding.

## B. Matrice agente → skill

`requirement-traceability` definisce per tutti i ruoli il registro comune di requisiti, owner, stato e prove nei task articolati. `agent-configuration` si attiva soltanto quando si crea o aggiorna una specifica di ruolo; il suo passo di scrittura instrada ora a `writing-for-agents`. Per ogni agente le procedure restano nelle skills, non replicate nella specifica.

| Agente | Skills e trigger verificati | Input → output / confine |
|---|---|---|
| PromptAgent | `requirement-traceability`; `writing-for-agents` per scrivere/rivedere prompt; `grilling` per decisioni sostanziali aperte; `project-graph-context` se servono destinatari o dipendenze. | Richiesta e decisioni confermate → prompt preciso e handoff; non esegue il task né modifica file. |
| AppStarter | `agent-configuration` per cambiare istruzioni; `grilling` e `codebase-design` su scelte iniziali aperte; `safe-refactor` per riordino autorizzato; `investigate-first` se struttura/avvio sono incerti; `verify-and-stop` solo per verifica richiesta; grafo se utile. | Stato NEW/EXISTING/RUNNING e progetto → bootstrap o piano circoscritto, con evidenze e compatibilità; non presume stack. |
| Architect | `agent-configuration`; `grilling` per vincoli architetturali aperti; `codebase-design` per contratti/confini; `safe-refactor` per valutare piani di riordino; grafo se utile. | Requisiti, struttura e prove → decisioni/contratti e owner; resta in sola lettura. |
| Backend | `agent-configuration`; `codebase-design` per interfacce locali; `investigate-first` o `diagnosing-bugs` secondo incertezza/complessità; `surgical-patch` per fix circoscritto; `safe-refactor` per riordino autorizzato; `verify-and-stop` su richiesta; grafo se utile. | Requisiti e contratto → modifiche di API, logica, dati o integrazioni nella propria area. |
| Frontend | Come Backend per diagnosi, patch, riordino e verifica; `codebase-design` per componenti/stato; graph context per flussi UI/API trasversali. | Requisiti e contratto API → UI e integrazione nella propria area; mock non prova l'integrazione server. |
| AIEngineer | `writing-for-agents` per prompt/orchestrazione; `grilling` su obiettivo/fonti/compromessi aperti; `codebase-design` per interfacce AI; `investigate-first` o `diagnosing-bugs`; `surgical-patch`, `safe-refactor`, `verify-and-stop`; `pipeline-benchmark` per preparare il passaggio a Evaluation; grafo se utile. | Requisiti, fonti e contratti → prompt, estrazione, retrieval o orchestration; Evaluation misura, AIEngineer non attribuisce benchmark. |
| Evaluation | `pipeline-benchmark` come procedura principale; `project-graph-context` per casi di handoff/ownership; `grilling` solo per gates/budget sostanzialmente aperti; `investigate-first` e `surgical-patch` solo sul proprio runner; `verify-and-stop` per artefatti. | Versioni, casi, rubriche, tracce e budget → BenchmarkReport con misure o limiti espliciti; non modifica prompt congelati. |
| AgentOptimizer | `writing-for-agents` per revisioni; `project-graph-context` per relazioni; `grilling` per conflitti di responsabilità; `retro` solo su richiesta; `verify-and-stop` e `pipeline-benchmark` per controllo e prova successiva. | Specifiche canoniche e report versionati → revisioni mirate/candidate; non installa modifiche in progetti esterni. |
| Reviewer | `verify-and-stop` per letture ammesse; `codebase-design` per contratti; `writing-for-agents` su prompt/skills; `surgical-patch` e `safe-refactor` come criteri, non come permesso di scrittura; `pipeline-benchmark` per report benchmark; grafo se utile. | Diff, criteri ed evidenze → findings al responsabile; resta in sola lettura. |

### Skills canoniche e input/output

| Skill | Attivazione e utilizzatori | Input → output | Fonte |
|---|---|---|---|
| `agent-configuration` | Creare/aggiornare un agente equivalente; tutti i ruoli solo in questa fase. | Specifica, ambiente e personalizzazioni → istruzioni o differenze motivate. Durante la stesura richiama `writing-for-agents`; se si crea una skill richiede `SKILL-MECHANICS.md`. | `Skills/agent-configuration/SKILL.md` |
| `requirement-traceability` | Task articolati o passaggi tra ruoli; per task semplici basta una checklist breve. | Richiesta e stato → requisiti, criteri, owner, dipendenze, evidenze e handoff conservati. Instrada handoff/retro solo su richiesta. | `Skills/requirement-traceability/SKILL.md` |
| `project-graph-context` | Link, dipendenze o impatto trasversale pertinenti. | Grafo e Markdown → relazioni, condizioni e contratti verificati nel testo. | `Skills/project-graph-context/SKILL.md` |
| `pipeline-benchmark` | Evaluation misura; AIEngineer prepara baseline/candidata; AgentOptimizer definisce prova successiva; Reviewer legge il report. | Casi, versioni, rubriche, tracce → confronto/report con metriche mancanti esplicite. | `Skills/pipeline-benchmark/SKILL.md` |
| `grilling` | Decisione importante non ricavabile dai file; non per requisiti già chiari. | Obiettivo e punti aperti → domande a tappe e decisioni confermate; PRD solo se richiesto. | `Skills/grilling/SKILL.md` |
| `handoff` | Solo quando viene chiesta una nuova sessione; consegne ordinarie restano nel TaskState. | Stato e artefatti → breve pacchetto self-contained con requisiti e riferimenti. | `Skills/handoff/SKILL.md` |
| `writing-for-agents` | Scrittura/revisione di prompt, skills o istruzioni. | Requisiti e testo → istruzioni con trigger, puntatori, criteri e meno duplicazioni. Legge `SKILL-MECHANICS.md` solo nella creazione di una skill. | `Skills/writing-for-agents/SKILL.md` |
| `codebase-design` | Confini, interfacce, dipendenze o testabilità da progettare/verificare. | Requisiti e struttura → contratti/confini proporzionati; gli agenti read-only non applicano cambi. | `Skills/codebase-design/SKILL.md` |
| `diagnosing-bugs` | Bug difficile/intermittente dopo l'indagine iniziale. | Sintomo e prove → diagnosi riproducibile e fix proposto nei limiti del ruolo. | `Skills/diagnosing-bugs/SKILL.md` |
| `retro` | Retrospettiva esplicitamente richiesta. | Sessione/artefatti autorizzati → ipotesi di miglioramento, non risultato di benchmark. | `Skills/retro/SKILL.md` |
| `investigate-first` | Causa incerta nell'area posseduta o nel runner Evaluation. | Sintomo e fonti → fatti, ipotesi separate e prossima indagine mirata. | `Skills/investigate-first/SKILL.md` |
| `surgical-patch` | Correzione localizzata dall'owner; per Reviewer solo criteri, per Evaluation solo il proprio runner. | Difetto e prove → patch minima oppure findings, rispettando permessi. | `Skills/surgical-patch/SKILL.md` |
| `safe-refactor` | Riordino richiesto; Architect pianifica, Reviewer valuta, owner implementa. | Baseline e dipendenze → piano/modifica reversibile con compatibilità. | `Skills/safe-refactor/SKILL.md` |
| `verify-and-stop` | Verifica richiesta o criterio assegnato. | Criteri e prove disponibili → esito per criterio, limiti e condizione di stop. | `Skills/verify-and-stop/SKILL.md` |

## C. Correzioni applicate

| Finding | File aggiornati | Esito |
|---|---|---|
| F1: PromptAgent locale ometteva la skill di progettazione quando crea/revisiona agenti o skills. | `.codex/agents/prompt-agent.toml` | Aggiunto trigger condizionale a `agent-design`; esclusi i prompt operativi ordinari. |
| F2: `agent-configuration` non instradava la fase di stesura. | `Skills/agent-configuration/SKILL.md` e copie App Starter, Full Stack, Evaluation. | Inserito richiamo a `writing-for-agents`; `SKILL-MECHANICS.md` soltanto per creare una skill. |
| F3: due README citavano Evaluation come incluso nei pack di sviluppo. | README App Starter e Full Stack. | Dichiarato che Evaluation non è incluso e collegato al pack dedicato. |
| F4: il catalogo `pipeline-benchmark` ometteva AIEngineer e Reviewer. | `Skills/README.md` e copie pack. | Distinte preparazione del confronto, misurazione e review read-only. |
| F5: i PROMPTME non installavano i ruoli/skills nel repository software di destinazione. | PROMPTME, WORKFLOW e README di App Starter, Full Stack ed Evaluation; README radice `Starter_pack/`. | Aggiunta rilevazione del coding runtime, creazione delle cartelle mancanti, adattamento locale, controllo conflitti, dipendenze e verifica effettiva. |
| F6: Evaluation e AgentOptimizer potevano essere confusi nella destinazione. | PROMPTME, WORKFLOW e README di Evaluation; README radice `Starter_pack/`. | Evaluation viene installato nel progetto valutato; AgentOptimizer resta nel repository canonico. |
| F7: “installare agenti nell'app” poteva riferirsi al runtime di produzione. | PROMPTME/WORKFLOW/README dei pack software, README radice. | Chiarito che si configura l'assistente di coding sul repository, non il runtime AI dell'app né le sue dipendenze. |
| F8: il catalogo portabile e il README pack collegavano il prodotto al laboratorio `.codex`. | `Skills/README.md`, `Starter_pack/README.md`, copie pack di `Skills/README.md`. | Rimossi link al laboratorio; i cataloghi nei pack rimandano al proprio `WORKFLOW.md`. I percorsi `.codex/agents/` citati sono l'adattamento condizionale del Codex di destinazione, non una dipendenza dai file del laboratorio. |

Le specifiche canoniche dei nove agenti portabili non sono state riscritte: la verifica statica le ha trovate già dotate di routing condizionale e limiti appropriati. Gli adattatori specifici di runtime vengono generati dalla chat di installazione, partendo da tali specifiche e non diventano fonti canoniche concorrenti.

## D. Installazione runtime documentata

| Runtime | File agenti di progetto | Skills di progetto | Indicazioni implementate nei PROMPTME |
|---|---|---|---|
| Codex | `.codex/agents/<nome>.toml`; campi richiesti `name`, `description`, `developer_instructions`. | `.agents/skills/<nome-skill>/SKILL.md` con risorse della skill. | Costruire TOML dal corpo canonico, adattare i link, lasciare percorsi globali intatti; riavviare se nuove skills non appaiono. |
| Claude Code | `.claude/agents/<nome>.md`; frontmatter con `name` e `description`, altri campi solo se documentati/supportati. | `.claude/skills/<nome-skill>/SKILL.md` e risorse. | Non pre-caricare indiscriminatamente `skills:` perché inserisce il testo completo; i subagents non ereditano la cronologia, quindi l'handoff è autonomo. Se la prima cartella `.claude/agents/` nasce durante la sessione, documentazione richiede un riavvio per rilevarla. |
| Altro o non determinato | Solo l'adattamento documentato dal runtime rilevato. | Solo il percorso/formato documentato. | Nessun formato inventato; se il runtime non è identificabile, si completa l'analisi indipendente e si chiede solo la decisione che cambia il formato. |

Riferimenti ufficiali consultati il 13 ottobre 2026: [Codex subagents](https://developers.openai.com/codex/subagents), [Codex skills](https://developers.openai.com/codex/skills), [Claude Code subagents](https://code.claude.com/docs/en/sub-agents), [Claude Code skills](https://code.claude.com/docs/en/skills). I dettagli di cartelle e frontmatter sono adattatori specifici del runtime; `Agents/` e `Skills/` canonici restano portabili.

## E. Verifiche e limiti

- La matrice è statica: controlla le istruzioni e gli archi Markdown, non dimostra agenti eseguiti in sequenza.
- I report storici in `Agents/` non sono stati contati come agenti.
- Controllo link: 132 file Markdown e 539 link relativi verificati; nessun percorso non risolto. I tre link errati rilevati nel report storico sono stati corretti.
- Metadati canonici: tutti i 14 `SKILL.md` hanno frontmatter con `name` corrispondente alla cartella e `description` presente. Il TOML del PromptAgent locale modificato è stato analizzato con `tomllib`.
- Integrità dei pack: 102 file inclusi in App Starter, Full Stack ed Evaluation confrontati tramite SHA-256 con le fonti canoniche; nessuna differenza o fonte mancante. I README delle skills nei pack hanno i link relativi adattati al proprio `WORKFLOW.md`.
- Separazione: nessun percorso alle skills/ruoli locali `.codex` né ID `lab_*` è stato trovato nei prodotti esportabili. I riferimenti a `.codex/agents/` nei prompt di installazione indicano solo la configurazione del Codex nel repository di destinazione.
- Nessun progetto software esterno era disponibile; perciò non sono state create le sue cartelle runtime né verificata la scoperta dei ruoli da Codex o Claude Code.
- Non sono state eseguite pipeline o test applicativi. Non si misurano costo, token, latenza, affidabilità o interventi umani.
- La disponibilità effettiva degli strumenti, la sicurezza del progetto di destinazione e i conflitti con agenti esistenti vanno verificati nella chat che applicherà PROMPTME.
- Le modifiche ai prompt/README e i controlli statici non provano miglioramento operativo; quest'ultimo richiede i casi e le trace del pack Evaluation.
