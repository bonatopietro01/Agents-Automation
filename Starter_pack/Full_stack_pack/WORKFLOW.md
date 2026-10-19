# Collaborazione e regole comuni

I file in Agents/ sono specifiche di ruolo; le cartelle in Skills/ contengono procedure e risorse. Leggi le specifiche disponibili e seleziona le skills secondo le sezioni "Skills per il task". Copiare i file non attiva automaticamente un runtime.

La chat principale coordina richiesta, scope, fonti autorizzate e TaskState: requisiti R1..., criteri, owner, dipendenze, decisioni, stato ed evidenze. Mantieni anche i requisiti bloccati e non applicabili con un motivo. Ogni consegna esplicita obiettivo, requisiti, file, permessi, skills necessarie, risultato atteso e destinatario. Ogni file condiviso ha un owner. Prima di attività parallele fissa contratti e confini.

Quando presente, AppStarter distingue NEW, EXISTING e RUNNING. Architect propone decisioni trasversali in sola lettura. Backend, Frontend e AIEngineer implementano soltanto nelle aree realmente presenti. Reviewer conclude in sola lettura; i rilievi tornano all'owner. Non serve coinvolgere tutti i ruoli per ogni richiesta.

Grilling chiarisce decisioni importanti aperte con round di domande e proposte consigliate; i fatti accessibili si ricavano dai file. I passaggi ordinari mantengono TaskState; handoff a nuova sessione e retro richiedono invocazione esplicita secondo il programma; non sono parte automatica della consegna ordinaria. Grafi e indici sono supporti da confermare nel sorgente.

Dati creati o trasformati devono mantenere schema, origine, trasformazioni, owner e distinzione reale/sintetico. Seleziona le risorse della skill necessarie al caso e segnala dipendenze indisponibili. Mantieni permessi dei ruoli e istruzioni del progetto.

Evaluation misura le pipeline con versioni, casi e condizioni fissi e salva BenchmarkReport.md. AgentOptimizer usa quel report nel repository canonico per revisioni mirate e salva OptimizationReport.md. Nei progetti con runtime installato i report vanno in `agent-kit/reports/` o nella directory report già designata, fuori da `.codex/agents/`, `.claude/agents/` e `.cursor/agents/`; per semplici raccolte di specifiche possono restare nella cartella degli agenti se pertinente e non usata per discovery. Non correggere i prompt mentre sono sotto confronto. Una modifica senza benchmark resta da validare; misure mancanti non diventano zero.

Non aggiungere né eseguire test senza una richiesta di testare o verificare. La richiesta di benchmark autorizza le prove pertinenti entro scope e budget stabiliti. Non introdurre implicitamente deploy, operazioni distruttive o cambiamenti all'istanza attiva. Distingui analisi statica, ruoli applicati nella chat e agenti eseguiti realmente.

Questi file sono copie esportate delle fonti canoniche del repository PROMPT_AGENTI. Le personalizzazioni appartengono al progetto di destinazione; gli aggiornamenti del repository non si propagano automaticamente.
Quando incluso, PromptAgent si attiva per richieste esplicite di creare o migliorare prompt. Le decisioni raccolte con grilling alimentano il prompt finale dopo la conferma; PRD soltanto se richiesto, salvataggio al coordinatore autorizzato. Per tool o delega mancanti applica la diagnosi di requirement-traceability e blocca soltanto le attività dipendenti.

Per richieste che analizzano la collaborazione nel grafo Obsidian usa project-graph-context e il riferimento obsidian-workflow.md: segui i link dei Markdown, verifica condizioni e contratti, distingui fonti canoniche e copie. Il grafo documenta relazioni; Evaluation confronta quelle relazioni con i passaggi osservati senza riscrivere i prompt congelati.

## Chiamare ruoli, skills e risorse

Il coordinatore delega usando il nome registrato dal manifest e gli strumenti esposti dalla sessione; non inventa funzioni o parametri. Il ruolo invoca la skill selezionata con il meccanismo disponibile e ne legge le risorse pertinenti: queste tre operazioni non sono intercambiabili. In Claude Code verifica l'accesso a Skill; non precaricare handoff/retro o skills condizionali. In Codex i permessi sono quelli della sessione: la sola lettura resta un vincolo del ruolo, non una sandbox separata garantita dal TOML. Usa i riferimenti dei tre adattamenti in agent-configuration per dettagli e diagnosi.

## Installazione nel progetto di destinazione

Segui [PROMPTME.md](PROMPTME.md): identifica progetto e pack, verifica Python 3.11+, esegui il generatore in anteprima, risolvi i conflitti, usa --apply e poi --check. I tre ambienti vengono preparati sempre: `.codex/agents/`, `.claude/agents/`, `.cursor/agents/`; le 14 skills complete sono in `.agents/skills/` e `.claude/skills/`, con contenuti equivalenti. Non creare percorsi globali e non installare questi ruoli nel runtime AI dell'applicazione.

Il manifest `agent-kit/INSTALLATION.json` registra fonti, nomi e hash. Le sezioni delimitate in AGENTS.md e CLAUDE.md collegano il coordinamento senza rimpiazzare istruzioni esistenti. File personalizzati e copie divergenti richiedono una risoluzione esplicita; non sono aggiornamenti automatici. Consulta [installation.md](Skills/agent-configuration/references/installation.md) per il contratto del generatore.

Prima del lavoro dipendente verifica il riconoscimento nel programma disponibile secondo [runtime-check.md](Skills/agent-configuration/references/runtime-check.md). Un errore richiede diagnosi di nome, formato, percorso, permessi, versione e caricamento prima di riprovare. Distingui file generati, controlli statici, elementi riconosciuti e chiamate provate. Gli ambienti assenti restano non verificati; non sostituire silenziosamente un agente con l'applicazione del ruolo nella stessa chat.
