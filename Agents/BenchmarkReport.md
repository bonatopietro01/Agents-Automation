# Benchmark della manutenzione locale PROMPT_AGENTI

## Sintesi

**Modalità:** `ANALISI_STATICA` · **Stato:** `PARTIAL` · **Raccomandazione:** `DATI INSUFFICIENTI`.

Ho esaminato i contratti degli agenti, le skills, i prompt, i pack, i link Markdown e la mappa Mermaid. Ho aggiunto un RepositoryMaintainer e una skill di manutenzione riservati a questo repository. Le dieci prove sotto verificano copertura documentale e isolamento dei pack; non sono esecuzioni della pipeline di agenti.

## Requisiti

| ID | Criterio | Esito |
|---|---|---|
| R1 | Agente locale con identità, attivazione, limiti, modalità e handoff. | Soddisfatto staticamente. |
| R2 | Skill locale con nome, procedura, dipendenze condizionali e formato canonico. | Soddisfatto staticamente. |
| R3 | Un prompt di ingresso distingue analisi, valutazione e modifiche autorizzate. | Soddisfatto staticamente. |
| R4 | README e catalogo distinguono strumenti locali da materiali portabili; Mermaid mostra flusso e routing. | Soddisfatto staticamente. |
| R5 | Link, dipendenze, conteggi, pack e casi sono controllati. | Controlli statici eseguiti; limiti sotto riportati. |
| R6 | Le dieci situazioni richieste sono confrontate con le istruzioni disponibili. | Copertura documentale verificata; comportamento non eseguito. |
| R7 | Report benchmark, aggiornamento storico e review indipendente. | Review indipendente completata; rilievi sul formato corretti e registrati. |

## Versioni e condizioni

```yaml
schema_version: agent-benchmark/v1
report_id: prompt-agenti-maintenance-2026-10-11
project_id: PROMPT_AGENTI
evidence_mode: ANALISI_STATICA
execution_status: PARTIAL
versions:
  project_revision: working-tree senza Git
  baseline: snapshot iniziale SHA-256 4C02443EFA775BC74D1A23106E2F1502A99CFEDA2239C77AA334A24B6B7B2DB1, 167 file
  candidate: RepositoryMaintainer 085FB964C8B4922C2281927BD6F44E8B59A02E457A1B98408F49119EEED2E8DE; skill 73E14FF1BC3727C1EB1DBE58A9C3D1A2CA874E77297F44C0151070F4D3C72B67; prompt DBEA525588BF62E854DBEDAEDD7868602F4747770395120283C61E1372C4E8B1
  dataset: checklist documentale sintetica C1-C10; nessun dataset eseguibile creato
  rubric: requisiti del prompt fornito dall'utente; confronto statico con le fonti e i file risultanti
agent_map:
  - name: RepositoryMaintainer
    role: coordinamento locale del repository
    path: Agents/RepositoryMaintainerAgent.md
    origin: locale, escluso dai pack
    revision: SHA-256 085FB964C8B4922C2281927BD6F44E8B59A02E457A1B98408F49119EEED2E8DE
  - name: PromptAgent
    role: creazione e revisione di prompt
    path: Agents/PromptAgent_General.md
    origin: canonica portabile; invariata
    revision: SHA-256 817E3DFF2373F38AA9F5248BDD8848AF9BFDBDDE0692497E3E2131A2317088E3
  - name: AppStarter
    role: avvio o riordino di applicazioni
    path: Agents/AppStarterAgent_General.md
    origin: canonica portabile; invariata
    revision: SHA-256 51471ADDEBD799544D16B786843BB6B488F7FF8569AB66102C51C9EF95F9F714
  - name: Architect
    role: decisioni architetturali trasversali
    path: Agents/ArchitectAgent_General.md
    origin: canonica portabile; invariata
    revision: SHA-256 9EE3DBFBD62B53B390C80490C9771E6493B52CC1DE2FE641BDD4111806552E7D
  - name: Backend
    role: backend e contratti server
    path: Agents/BackendAgent_General.md
    origin: canonica portabile; invariata
    revision: SHA-256 F1447821A8571BEFB41167AAB7E49A4769DB712F31DFF075E57E2A09F55C0D42
  - name: Frontend
    role: UI e client API
    path: Agents/FrontendAgent_General.md
    origin: canonica portabile; invariata
    revision: SHA-256 B8D20B43131A80C0C9978B84E2A46F8B8CC24B4DA44F9393E1A407808134ED79
  - name: AIEngineer
    role: AI e orchestrazione
    path: Agents/AIEngineerAgent_General.md
    origin: canonica portabile; invariata
    revision: SHA-256 0D332854D589DC92DFDB59791374203D2464A9EAFC70A05407127EE24AF5FEEB
  - name: Reviewer
    role: review finale in sola lettura
    path: Agents/ReviewerAgent_General.md
    origin: canonica portabile; invariata
    revision: SHA-256 4FB1A3BEE61C603166522A479C535984C5D575D4A6C252EE8DA1B204F806C097
  - name: Evaluation
    role: benchmark e report del progetto
    path: Agents/EvaluationAgent_General.md
    origin: canonica portabile; invariata
    revision: SHA-256 B5A98E13EB11524EB377A0794C1E11FF272020A42152A149385E208E864467FE
  - name: AgentOptimizer
    role: miglioramento dei prompt canonici
    path: Agents/AgentOptimizerAgent_General.md
    origin: canonica portabile; invariata
    revision: SHA-256 84989919ABE7C4F10A9F0F8185FB2C9E5BAA70B12E15B4D55232114B5C217992
workflow:
  - relazione documentata nei Markdown e nei diagrammi Mermaid
  - nessun runner della pipeline trovato nel repository
conditions:
  - nessun provider/modello o runner del progetto disponibile per eseguire i ruoli come pipeline
  - link Markdown risolti relativamente ai file; ancore confrontate con le intestazioni
  - pack confrontati con le fonti canoniche; personalizzazioni documentali dei pack preservate
predefined_gates:
  - RepositoryMaintainer e la skill locale non compaiono nei pack
  - le 14 skills portabili e gli agenti previsti sono presenti nei pack
  - nessun nuovo difetto critico dimostrato; un controllo statico non basta a promuovere prestazioni
cases:
  - case_id: C1
    origin: sintetico
    category: prompt-only
    requirements: [R6]
    input: "Scrivi un prompt per creare una dashboard; non costruire la dashboard."
    allowed_context: [richiesta sintetica, specifica PromptAgent]
    initial_state: "PromptAgent e ruoli software canonici presenti; nessuna richiesta di implementazione."
    rubric: "PromptAgent produce un prompt pronto da usare e si ferma; non avvia gli agenti software."
    artifact_ref: [Agents/PromptAgent_General.md]
    controls:
      deterministic: ["output contiene un prompt utilizzabile", "nessun file applicativo dichiarato come creato"]
      error_checks:
        critical: ["non eseguire il task descritto nel prompt"]
        major: ["non attivare ruoli di sviluppo senza richiesta"]
    result: COPERTO_NELLA_SPECIFICA
  - case_id: C2
    origin: sintetico
    category: grilling-and-prd
    requirements: [R6]
    input: "Aiutami a definire un agente per supportare un team; non ho ancora deciso utenti, limiti o formato."
    allowed_context: [richiesta sintetica, Skills/grilling/SKILL.md, specifica PromptAgent]
    initial_state: "Requisiti essenziali aperti; nessuna autorizzazione a creare o salvare un PRD."
    rubric: "PromptAgent fa domande mirate a round, mantiene le decisioni e chiede conferma prima del prompt finale; crea un PRD solo se richiesto."
    artifact_ref: [Skills/grilling/SKILL.md, Agents/PromptAgent_General.md, Skills/requirement-traceability/SKILL.md]
    controls:
      deterministic: ["domande raggruppate per decisione", "conferma prima del prompt finale"]
      error_checks:
        critical: ["non inventare risposte"]
        major: ["non trattare un PRD come output automatico"]
    result: COPERTO_NELLA_SPECIFICA
  - case_id: C3
    origin: sintetico
    category: local-routing
    requirements: [R1, R2, R6]
    input: "Aggiungi un agente locale che mantenga questo catalogo e non venga esportato nei pack."
    allowed_context: [richiesta sintetica, README.md, Agents/RepositoryMaintainerAgent.md, skill locale, workflow dei pack]
    initial_state: "Repository canonico con ruoli portabili e pack esportabili; owner dei file da dichiarare prima delle modifiche."
    rubric: "RepositoryMaintainer instrada solo i ruoli/skills pertinenti, assegna owner e mantiene agente e skill locali fuori dai pack."
    artifact_ref: [Agents/RepositoryMaintainerAgent.md, Skills/prompt-repository-maintenance/SKILL.md, README.md, Starter_pack/README.md]
    controls:
      deterministic: ["agente e skill locali assenti dagli inventari dei pack", "owner e percorsi previsti indicati"]
      error_checks:
        critical: ["non esportare l'agente o la skill locali nei pack"]
        major: ["non modificare ruoli canonici fuori scope", "assegnare owner ai file coinvolti"]
    result: COPERTO_NELLA_SPECIFICA
  - case_id: C4
    origin: sintetico
    category: specialist-handoff
    requirements: [R6]
    input: "Implementa una schermata che usa un nuovo endpoint e una risposta AI."
    allowed_context: [richiesta sintetica, agenti Architect/Backend/Frontend/AIEngineer/Reviewer, skills di traceability]
    initial_state: "L'attività coinvolge UI, API e AI; contratti e criteri non sono ancora definiti."
    rubric: "I ruoli pertinenti concordano i confini; gli stessi requirement ID, contratti e prove arrivano al Reviewer in sola lettura."
    artifact_ref: [Agents/ArchitectAgent_General.md, Agents/BackendAgent_General.md, Agents/FrontendAgent_General.md, Agents/AIEngineerAgent_General.md, Agents/ReviewerAgent_General.md, Skills/requirement-traceability/SKILL.md]
    controls:
      deterministic: ["ogni requisito ha un ID tracciabile", "reviewer riceve criteri, aree e prove"]
      error_checks:
        critical: ["non perdere requisiti nell'handoff", "reviewer non modifica i file"]
        major: ["contratti condivisi e ownership esplicitati"]
    result: COPERTO_NELLA_SPECIFICA
  - case_id: C5
    origin: sintetico
    category: missing-capability
    requirements: [R2, R6]
    input: "Usa il grafo del progetto per trovare il componente, ma il vault o la skill grafo non sono accessibili."
    allowed_context: [richiesta sintetica, istruzioni disponibili localmente]
    initial_state: "Grafo/tool dichiarato non disponibile; accesso ai file locali consentito."
    rubric: "L'agente dichiara il limite e applica un fallback documentale verificabile senza affermare di aver interrogato il grafo."
    artifact_ref: [Skills/project-graph-context/SKILL.md, Skills/requirement-traceability/SKILL.md]
    controls:
      deterministic: ["limite esplicito", "fallback e fonti nominati"]
      error_checks:
        critical: ["non dichiarare una consultazione del grafo non avvenuta", "non presentare risultati non verificati come fatti"]
        major: ["indicare il fallback disponibile"]
    result: COPERTO_NELLA_SPECIFICA
  - case_id: C6
    origin: sintetico
    category: explicit-skill-invocation
    requirements: [R2, R6]
    input: 'Esegui un handoff; in una prova separata chiedi "fai una retrospettiva".'
    allowed_context: [richieste sintetiche, frontmatter e corpi delle due skills]
    initial_state: "Skills handoff e retro disponibili, ma non attivate nel task precedente."
    rubric: "Ogni procedura parte quando richiesta e segue i propri input e criteri d'uscita."
    artifact_ref: [Skills/handoff/SKILL.md, Skills/retro/SKILL.md, Skills/requirement-traceability/SKILL.md]
    controls:
      deterministic: ["trigger esplicito presente", "risultato segue la procedura documentata"]
      error_checks:
        critical: ["non dichiarare completata una procedura senza il risultato richiesto"]
        major: ["nessuna attivazione implicita"]
    result: COPERTO_NELLA_SPECIFICA
  - case_id: C7
    origin: sintetico
    category: cover-letter-evidence
    requirements: [R6]
    input: "Genera una cover letter da un CV, dalle risposte della persona e da due lettere di esempio."
    allowed_context: [CV sintetico, risposte sintetiche, esempi usati solo come riferimento stilistico, prompt canonico e pack]
    initial_state: "I fatti del candidato provengono da CV/risposte; gli esempi non sono fonti biografiche."
    rubric: "La lettera usa soltanto fatti supportati dal CV o dalle risposte e usa gli esempi per lo stile."
    artifact_ref: [Prompts/CoverLetter.md, Starter_pack/Cover_letter_Pack/PROMPTME.md]
    controls:
      deterministic: ["fonti di contesto etichettate per ruolo", "istruzione vieta di copiare fatti dagli esempi"]
      error_checks:
        critical: ["nessun fatto candidato inventato"]
        major: ["nessuna esperienza di esempio attribuita al candidato"]
    result: COPERTO_NELLA_SPECIFICA
  - case_id: C8
    origin: sintetico
    category: cover-letter-character-limit
    requirements: [R6]
    input: "Crea le istruzioni personalizzate finali del progetto Cover Letter."
    allowed_context: [requisiti sintetici della persona, prompt canonico e pack]
    initial_state: "Non è stato ancora generato un testo personalizzato finale da misurare."
    rubric: "Il prompt richiede un conteggio automatico sul testo finale e una lunghezza inferiore a 8.000 caratteri."
    artifact_ref: [Prompts/CoverLetter.md, Starter_pack/Cover_letter_Pack/PROMPTME.md]
    controls:
      deterministic: ["regola di conteggio presente", "conteggio finale verificabile con script"]
      error_checks:
        critical: ["non dichiarare una lunghezza misurata quando non esiste output finale"]
        major: ["indicare il limite di caratteri richiesto"]
    result: SPECIFICA_PRESENTE; conteggio di output finale non eseguito
  - case_id: C9
    origin: sintetico
    category: evaluation-optimizer-loop
    requirements: [R5, R6]
    input: "Valuta una modifica a un agente e passa i finding all'Optimizer per una candidata."
    allowed_context: [richiesta sintetica, Evaluation, AgentOptimizer, pipeline-benchmark, dataset autorizzato se esistente]
    initial_state: "È disponibile una candidata documentale ma non un runner; baseline/runtime e telemetria devono essere verificati."
    rubric: "Evaluation conserva versioni, casi e limiti; Optimizer modifica solo sulla base dei finding e la candidata viene rivalutata sugli stessi casi."
    artifact_ref: [Agents/EvaluationAgent_General.md, Agents/AgentOptimizerAgent_General.md, Skills/pipeline-benchmark/SKILL.md]
    controls:
      deterministic: ["versioni identificate", "stesso dataset richiesto per il confronto", "metriche non misurate esplicitate"]
      error_checks:
        critical: ["nessun benchmark runtime simulato", "nessuna promozione su dati insufficienti"]
        major: ["run e finding collegati alle evidenze"]
    result: COPERTO_NELLA_SPECIFICA
  - case_id: C10
    origin: sintetico
    category: export-isolation
    requirements: [R1, R2, R4, R5]
    input: "Esporta i pack software/Evaluation e Cover Letter dopo aver aggiunto gli strumenti locali di manutenzione."
    allowed_context: [inventario canonico, quattro cartelle Starter_pack, copie degli agenti e skills]
    initial_state: "Un RepositoryMaintainer e una skill di manutenzione locali sono presenti nel canonico; pack esportabili già esistenti."
    rubric: "I pack non contengono né richiamano i componenti locali; le copie portabili corrispondono ai canonici."
    artifact_ref: [Agents/RepositoryMaintainerAgent.md, Skills/prompt-repository-maintenance/SKILL.md, Starter_pack/README.md]
    controls:
      deterministic: ["confronto SHA-256 delle copie", "ricerca di nomi e percorsi locali in ogni pack"]
      error_checks:
        critical: ["nessun file o richiamo locale nei pack"]
        major: ["nessuna copia divergente sovrascritta senza controllo"]
    result: VERIFICATO_STATICAMENTE
runs: [] # Nessuna esecuzione della pipeline o di ruoli distinti.
metrics:
  - name: static_scenario_coverage
    variant: candidate-static
    agent: repository-wide document review; no runtime agent invocation
    value: 10
    unit: casi esaminati
    status: COPERTURA_DOCUMENTALE
    n: 10
    method: confronto dei dieci scenari con le specifiche e i pack
    evidence_refs: [cases C1-C10]
    limit: nessuna esecuzione runtime
  - name: local_markdown_links
    variant: candidate-static
    agent: repository-wide link checker
    value: 486
    unit: riferimenti
    status: MISURATO_STATICAMENTE
    n: 122
    method: parser PowerShell, link Markdown e ancore sull'intero repository
    evidence_refs: [link check]
    limit: 31 link esterni esclusi; controllo locale di file/sezioni, non valida plugin Obsidian o render Mermaid
  - name: pack_role_copy_mismatches
    variant: candidate-static
    agent: repository-wide pack comparison
    value: 0
    unit: copie agente
    status: MISURATO_STATICAMENTE
    n: 15
    method: confronto dei ruoli inclusi nei tre pack contro i canonici
    evidence_refs: [inventario pack]
    limit: i componenti locali sono intenzionalmente esclusi
  - name: pack_skill_file_mismatches
    variant: candidate-static
    agent: repository-wide pack comparison
    value: 0
    unit: file skill
    status: MISURATO_STATICAMENTE
    n: 42
    method: confronto dei file nelle 14 skills portabili dei tre pack software/Evaluation
    evidence_refs: [inventario pack]
    limit: i cataloghi Skills/README.md dei pack hanno adattamenti documentali specifici
  - name: local_component_references_in_packs
    variant: candidate-static
    agent: repository-wide text search
    value: 0
    unit: riferimenti
    status: MISURATO_STATICAMENTE
    n: 4
    method: ricerca dei nomi dei due componenti nelle quattro cartelle pack
    evidence_refs: [C10]
    limit: verifica dei file, non attivazione runtime
  - name: task_success
    variant: baseline-and-candidate-runtime
    agent: all roles; not executed
    value: null
    unit: percento
    status: NON_MISURATO
    n: 0
    method: richiede esecuzioni della pipeline
    evidence_refs: []
    limit: runner assente
  - name: groundedness
    variant: baseline-and-candidate-runtime
    agent: all roles; not executed
    value: null
    unit: percento
    status: NON_MISURATO
    n: 0
    method: richiede output valutati e rubric
    evidence_refs: []
    limit: nessun output runtime
  - name: calls_per_job
    variant: baseline-and-candidate-runtime
    agent: all roles; not executed
    value: null
    unit: chiamate/job
    status: NON_MISURATO
    n: 0
    method: richiede tracing della pipeline
    evidence_refs: []
    limit: runner assente
  - name: tokens_per_job
    variant: baseline-and-candidate-runtime
    agent: all roles; not executed
    value: null
    unit: token input+output/job
    status: NON_MISURATO
    n: 0
    method: richiede token usage per chiamata
    evidence_refs: []
    limit: runner/provider usage assenti
  - name: cost_per_job
    variant: baseline-and-candidate-runtime
    agent: all roles; not executed
    value: null
    unit: costo/job
    status: NON_MISURATO
    n: 0
    method: richiede pricing e usage osservato
    evidence_refs: []
    limit: nessuna telemetria o prezzo configurato
  - name: latency_p50
    variant: baseline-and-candidate-runtime
    agent: all roles; not executed
    value: null
    unit: millisecondi
    status: NON_MISURATO
    n: 0
    method: richiede durata dei job
    evidence_refs: []
    limit: runner assente
  - name: latency_p95
    variant: baseline-and-candidate-runtime
    agent: all roles; not executed
    value: null
    unit: millisecondi
    status: NON_MISURATO
    n: 0
    method: richiede campione di durate dei job
    evidence_refs: []
    limit: runner e campione assenti
  - name: reliability
    variant: baseline-and-candidate-runtime
    agent: all roles; not executed
    value: null
    unit: percento job senza errori
    status: NON_MISURATO
    n: 0
    method: richiede esiti runtime ed errori per step
    evidence_refs: []
    limit: nessuna esecuzione osservata
  - name: human_edits
    variant: baseline-and-candidate-runtime
    agent: all roles; not executed
    value: null
    unit: percento output che richiede correzione
    status: NON_MISURATO
    n: 0
    method: richiede output e feedback umano raccolti
    evidence_refs: []
    limit: nessun output consegnato a valutatori
  - name: collaboration
    variant: baseline-and-candidate-runtime
    agent: all roles; not executed
    value: null
    unit: requisiti persi/handoff errati/routing duplicato per job
    status: NON_MISURATO
    n: 0
    method: richiede tracce di handoff e output dei passaggi
    evidence_refs: []
    limit: la copertura documentale non dimostra la collaborazione runtime
findings:
  - finding_id: F1
    case_id: C3
    run_id: null
    step_id: null
    agent: RepositoryMaintainer
    severity: media
    issue: mancava un ruolo locale per governare il repository
    change: creati agente, skill e prompt di ingresso locali
    evidence_refs: [Agents/RepositoryMaintainerAgent.md, Skills/prompt-repository-maintenance/SKILL.md, Prompts/ManutieniQuestoRepository.md]
    status: VERIFICATO_STATICAMENTE
  - finding_id: F2
    case_id: C10
    run_id: null
    step_id: null
    agent: RepositoryMaintainer
    severity: bassa
    issue: link errati e conteggi uguali nei cataloghi dei pack
    change: link e conteggi corretti nei tre cataloghi
    evidence_refs: [Starter_pack/Full_stack_pack/Skills/README.md, Starter_pack/App_starter_pack/Skills/README.md, Starter_pack/Evaluation_pack/Skills/README.md]
    status: APPLICATO
  - finding_id: F3
    case_id: C10
    run_id: null
    step_id: null
    agent: RepositoryMaintainer
    severity: bassa
    issue: tre link storici a Skills_Matt non risolvevano più
    change: riallineati ai percorsi Skills equivalenti
    evidence_refs: [Agents/OptimizationReport.md]
    status: APPLICATO
  - finding_id: F4
    case_id: C9
    run_id: null
    step_id: null
    agent: Evaluation/AgentOptimizer
    severity: bloccante_per_le_metriche
    issue: runner e telemetria assenti
    change: nessuna; riportati limiti e prova successiva
    evidence_refs: [Skills/pipeline-benchmark/SKILL.md, Agents/EvaluationAgent_General.md]
    status: APERTO
  - finding_id: F5
    case_id: C1-C10
    run_id: null
    step_id: null
    agent: Reviewer
    severity: media
    issue: la prima bozza non esplicitava input, contesto consentito, stato iniziale, artifact_ref e controlli per ogni caso
    change: completato lo schema descrittivo per tutti i casi; nessuna esecuzione runtime attribuita
    evidence_refs: [Agents/BenchmarkReport.md]
    status: RISOLTO_NEL_REPORT
  - finding_id: F6
    case_id: C1-C10
    run_id: null
    step_id: null
    agent: Reviewer
    severity: bassa
    issue: mancava una tabella narrativa baseline/candidata/differenza e l'esito della review
    change: aggiunta tabella comparativa con misure runtime N/A; registrata la review indipendente e mantenuta separata dalla validazione umana degli output
    evidence_refs: [Agents/BenchmarkReport.md, Agents/OptimizationReport.md]
    status: RISOLTO_NEL_REPORT
worsened_case_ids: [] # Non esiste un confronto dinamico baseline/candidata.
human_validation:
  - type: valutazione umana degli output runtime
    status: NOT_PERFORMED
    sample: []
    limits: "Nessuna persona ha valutato output runtime; la review indipendente era documentale e in sola lettura."
independent_review:
  status: COMPLETATA
  scope: "verifica documentale in sola lettura di isolamento, conteggi, collegamenti e conformità del report"
  findings: [F5, F6]
  resolution: "i campi dei casi, la tabella comparativa e gli stati sono stati aggiornati; runtime resta non misurato"
recommendation: DATI INSUFFICIENTI
next_experiments:
  - rendere disponibile un runner autorizzato con tracing reale
  - eseguire un pilot di 3-5 casi, poi lo stesso set baseline/candidata
  - verificare separatamente il conteggio di istruzioni Cover Letter personalizzate
limits:
  - nessun runner o pipeline di agenti esecutivi disponibile o eseguito; il Reviewer ha svolto soltanto una verifica documentale indipendente
  - nessuna misura di qualità o costi attribuibile ai ruoli
  - renderer Mermaid e interfaccia Obsidian non controllati
  - workspace.json cambiato rispetto allo snapshot; provenienza non determinata
```

## Confronto baseline/candidata

La baseline è lo snapshot iniziale; la candidata è la documentazione dopo le modifiche. Non esistono esecuzioni comparabili delle pipeline. Perciò le differenze di qualità, uso risorse e intervento umano sono `N/A — NON MISURATO`; i dieci casi sono copertura statica della sola candidata, non un miglioramento rispetto alla baseline.

| Metrica | Baseline | Candidata | Differenza | Stato |
|---|---|---|---|---|
| Task success | N/A | N/A | N/A | NON MISURATO: runner assente |
| Groundedness | N/A | N/A | N/A | NON MISURATO: nessun output runtime valutato |
| Calls/job | N/A | N/A | N/A | NON MISURATO: nessuna telemetria |
| Tokens/job | N/A | N/A | N/A | NON MISURATO: nessuna telemetria |
| Costo/job | N/A | N/A | N/A | NON MISURATO: nessun pricing/usage osservato |
| Latenza p50/p95 | N/A | N/A | N/A | NON MISURATO: nessuna durata osservata |
| Affidabilità/errori | N/A | N/A | N/A | NON MISURATO: nessuna esecuzione osservata |
| Human edits | N/A | N/A | N/A | NON MISURATO: nessun output consegnato a valutatori |
| Collaborazione e requisiti persi | N/A | N/A | N/A | NON MISURATO: nessuna traccia di handoff |
| Copertura documentale C1-C10 | Non rilevata con questa rubrica | 10 casi descritti e confrontati con le specifiche | Non confrontabile | Solo candidata; nessun pass runtime |

### Esito della review indipendente

Il Reviewer in sola lettura ha confermato l'isolamento dei componenti locali, i conteggi dei pack, i collegamenti verificati e la coerenza testuale dei diagrammi Mermaid. Ha richiesto campi descrittivi completi per C1-C10 e una tabella baseline/candidata/differenza. I due rilievi di conformità documentale (F5 e F6) sono stati corretti in questo report. La review non costituisce una valutazione umana della qualità degli output di una pipeline.

La baseline è stata conservata in uno snapshot temporaneo e usata per verificare le differenze. Non esiste una revisione Git del progetto. La verifica ha rilevato una modifica a `.obsidian/workspace.json` rispetto allo snapshot; non ho scritto quel file e l'ho lasciato intatto. `.obsidian/graph.json` è byte per byte identico allo snapshot.

## Inventario ed esportazione

| Area | Canonici | Pack | Controllo |
|---|---:|---:|---|
| Agenti portabili | 9 | Full Stack 6; App Starter 7; Evaluation 2; Cover Letter 0 | Copie dei ruoli presenti confrontate con gli originali: nessuna differenza. |
| Agenti locali | 1 | 0 | RepositoryMaintainer non compare nei contenuti dei pack. |
| Skills portabili | 14 | 14 in ciascun pack software/Evaluation | Risorse e file delle 14 cartelle confrontati: nessuna differenza. |
| Skills locali | 1 | 0 | La cartella locale è esclusa dai pack e non è richiamata dagli agenti portabili. |
| Cover Letter | 1 prompt canonico | PROMPTME della Cover Letter | Contenuto identico dopo normalizzazione delle sole terminazioni di riga. |

Ho aggiornato i cataloghi dei tre pack per puntare al loro `WORKFLOW.md` e riportare i conteggi di ruolo corretti (6, 7 e 2). I loro README di skills differiscono quindi dal catalogo canonico soltanto per le descrizioni e i collegamenti specifici del pack.

## Casi statici

I casi sono scenari sintetici ricavati dalla richiesta. `COPERTO` indica che il requisito è documentato e rintracciabile; non significa che un agente indipendente abbia eseguito il caso.

| Caso | Scenario | Evidenza verificata | Esito |
|---|---|---|---|
| C1 | L'utente chiede un prompt e PromptAgent scrive senza eseguire il lavoro descritto. | `Agents/PromptAgent_General.md`: identità, permessi, formato del prompt. | COPERTO |
| C2 | Grilling raccoglie decisioni e conferma; PRD soltanto se richiesto. | `Skills/grilling/SKILL.md`, sezione grilling di PromptAgent e traceability. | COPERTO |
| C3 | Un task locale coinvolge solo i ruoli necessari, con un owner per file. | RepositoryMaintainer, `Skills/requirement-traceability/SKILL.md`, `README.md` e `WORKFLOW.md` dei pack. | COPERTO |
| C4 | Backend, Frontend e AIEngineer trasferiscono contratti e R-ID fino alla review. | Link tra ruoli, handoff con ID nella traceability, Reviewer in sola lettura. | COPERTO |
| C5 | Skill, tool o grafo indisponibili producono un limite dichiarato e un fallback documentale. | Traceability, project-graph-context e istruzioni di fallback dei ruoli. | COPERTO |
| C6 | Handoff e retro si attivano solo nelle condizioni richieste. | Frontmatter delle due skills e riferimenti in requirement-traceability. | COPERTO |
| C7 | Cover letter usa CV e risposte per i fatti; esempi solo per lo stile; workflow previsto. | `Prompts/CoverLetter.md` e copia `Starter_pack/Cover_letter_Pack/PROMPTME.md`. | COPERTO |
| C8 | Il prompt Cover Letter richiede conteggio automatico delle istruzioni finali sotto 8.000 caratteri, con tetto 7.500. | Regola e procedura di conteggio presenti in entrambe le copie. Nessuna istruzione personalizzata è stata generata per misurarne la lunghezza effettiva. | COPERTO NELLA SPECIFICA |
| C9 | Evaluation consegna una candidata versionata ad AgentOptimizer e la rivalutazione usa gli stessi casi. | Ruoli Evaluation/AgentOptimizer, `pipeline-benchmark` e diagramma già esistente. | COPERTO |
| C10 | Il nuovo agente e la skill locali non contaminano esportazioni o agenti portabili. | Inventario dei quattro pack, riferimenti testuali e confronto delle copie. | VERIFICATO STATICAMENTE |

La nuova skill richiama le nove procedure richieste con condizioni esplicite: `agent-configuration`, `writing-for-agents`, `requirement-traceability`, `project-graph-context`, `pipeline-benchmark`, `verify-and-stop`, `grilling`, `handoff` e `retro`. I file e i riferimenti relativi esistono; handoff e retro restano espliciti.

## Controlli e metriche

| Controllo o metrica | Risultato | Metodo e limite |
|---|---|---|
| File Markdown esaminati | 122 | Inventario ricorsivo finale nel repository. |
| Link locali a file o sezioni | 486; 0 destinazioni mancanti | Parser PowerShell per link Markdown inline e ancore; 31 link esterni esclusi; non valida plugin Obsidian o render Mermaid. |
| Skills canoniche | 15; 0 errori di nome/frontmatter rilevati | Confronto `name` e cartella, presenza di `description` e `SKILL.md`. |
| Copie dei file skill nei pack | 0 differenze nei 14 pacchetti portabili | Confronto ricorsivo dei file dopo normalizzazione delle sole terminazioni di riga. I tre cataloghi pack hanno adattamenti locali espliciti. |
| Riferimenti ai componenti locali nei pack | 0 | Ricerca dei nomi del RepositoryMaintainer e della skill locale. |
| Recinti Markdown | 0 file con recinti non bilanciati | Conteggio dei delimitatori di codice Markdown. |
| Task success della pipeline | NON MISURATO | Nessun runner o pipeline reale disponibile. |
| Groundedness, chiamate, token, costo, latenza, affidabilità, modifiche umane, collaborazione | NON MISURATI | Nessuna esecuzione osservata, traccia di handoff o feedback umano. |
| Review indipendente dei materiali locali | COMPLETATA | Il Reviewer ha confermato isolamento, conteggi, collegamenti e diagrammi testuali; F5 e F6 corretti. Nessuna valutazione di output runtime. |

Non è stata eseguita alcuna chiamata a pagamento. L'applicazione dei ruoli nella stessa chat e il comportamento di un runner esterno non sono stati misurati.

## Findings e interventi

| ID | Evidenza | Intervento | Stato |
|---|---|---|---|
| F1 | La raccolta non aveva un ruolo locale per governare i propri file senza coinvolgere le specifiche portabili. | Creati RepositoryMaintainer, skill locale e prompt d'ingresso; i pack sono rimasti privi di tali riferimenti. | APPLICATO_DA_VALIDARE |
| F2 | I cataloghi dei pack puntavano a un'ancora del README canonico inesistente nei pack e attribuivano a ciascun pack lo stesso numero di agenti. | Link adattati al `WORKFLOW.md` incluso; conteggi corretti per i tre pack. | APPLICATO; link ricontrollati |
| F3 | Tre rimandi storici in `Agents/OptimizationReport.md` puntavano alla cartella rimossa `Skills_Matt/`. | Destinazioni riallineate alle cartelle canoniche equivalenti in `Skills/`; nota storica aggiornata, senza alterare dati o hash delle valutazioni precedenti. | APPLICATO; link ricontrollati |
| F4 | Nessun runner per la pipeline è disponibile in questo repository. | Nessuna modifica ai prompt congelati. Prima di decidere se promuovere modifiche di performance serve un runner autorizzato e telemetria. | NON RISOLTO; blocca metriche operative |

## File coinvolti

- Nuovi: `Agents/RepositoryMaintainerAgent.md`, `Skills/prompt-repository-maintenance/SKILL.md`, `Prompts/ManutieniQuestoRepository.md`, `Agents/BenchmarkReport.md`.
- Aggiornati: `README.md`, `Skills/README.md`, `Starter_pack/README.md`, i tre cataloghi `Starter_pack/*/Skills/README.md` e `Agents/OptimizationReport.md`.
- Nessuna specifica canonica portabile di agente o skill è stata modificata. I file in `.obsidian/` non sono stati scritti da questa revisione; il cambiamento di `workspace.json` resta di provenienza non determinata.

## Limiti e prossimo esperimento

Questa è una verifica documentale, non una prova di esecuzione indipendente. Mermaid è stato controllato a vista nel testo, senza renderer. La misura del limite Cover Letter richiede la generazione di istruzioni personalizzate reali; qui è stato verificato solo che il prompt imponga il controllo.

Per un benchmark delle prestazioni, serve rendere disponibili agenti eseguibili, versioni e tracciamento di chiamate, token, costi, durata, errori e interventi umani. Poi confrontare baseline e candidata su casi e condizioni fissi, iniziando da un pilot di 3–5 casi e ampliandolo quando dataset e budget lo consentono. Finché questi dati mancano, la raccomandazione resta `DATI INSUFFICIENTI`.
