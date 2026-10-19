# Evaluation pack: scegli la fase

Usa la fase 1 nel progetto software; trasferisci il report alla fase 2 nel repository canonico degli agenti. Copia il blocco della fase desiderata e rendi accessibile questo file completo. Non eseguire entrambe le fasi nel software valutato.

# Installazione e avvio

Leggi WORKFLOW.md, Skills/README.md e Skills/agent-configuration/SKILL.md di questo pack. Installa le configurazioni prima del lavoro dipendente. Le specifiche in Agents/ sono fonti da adattare; non dimostrano che un subagente sia già disponibile.

1. Identifica la radice del progetto di destinazione, la cartella completa del pack, le istruzioni esistenti e il programma effettivamente in uso. Conserva personalizzazioni, permessi e ruoli equivalenti. Non installare nel repository sorgente del laboratorio e non modificare configurazioni globali.
2. Verifica Python 3.11 o successivo. Se manca, indica il prerequisito e fermati sull'installazione senza scaricarlo automaticamente. Usa il generatore incluso; sostituisci i segnaposto con percorsi reali e mantieni le virgolette per percorsi con spazi:

   ```text
   python "<pack>/Skills/agent-configuration/scripts/install_agent_pack.py" --pack "<pack>" --project "<progetto>"
   python "<pack>/Skills/agent-configuration/scripts/install_agent_pack.py" --pack "<pack>" --project "<progetto>" --apply
   python "<pack>/Skills/agent-configuration/scripts/install_agent_pack.py" --pack "<pack>" --project "<progetto>" --check
   ```

   Esegui prima l'anteprima. Risolvi i conflitti segnalati prima delle scritture, preservando i file personalizzati; poi applica e controlla. Questa richiesta autorizza i controlli statici dell'installazione, non test indiscriminati dell'applicazione. Se non puoi eseguire comandi o scrivere file, consegna il limite e i passaggi necessari: non dichiarare l'installazione completata.
3. Prepara tutti e tre gli ambienti: agenti TOML in `.codex/agents/`, Markdown con frontmatter in `.claude/agents/` e `.cursor/agents/`; skills complete in `.agents/skills/` per Codex/Cursor e `.claude/skills/` per Claude Code. Il generatore include le 14 skills, metadati, dipendenze e risorse. Mantieni equivalenti le due copie: Cursor può leggerle entrambe; una divergenza dello stesso nome è un conflitto. Leggi i testi solo quando pertinenti, senza precaricare tutto.
4. Usa il manifest `agent-kit/INSTALLATION.json` per fonti, nomi registrati, percorsi e hash. Il generatore integra sezioni delimitate di coordinamento in AGENTS.md e CLAUDE.md e crea il workflow di coordinamento `agent-kit/WORKFLOW.md`, preservando il resto. Aggiorna automaticamente soltanto file propri invariati; non sovrascrivere personalizzazioni o configurazioni di altri pack.
5. Segui `Skills/agent-configuration/references/runtime-check.md` per verificare scoperta e chiamate nel programma disponibile. Usa il nome registrato e lo schema degli strumenti realmente esposti. Distinguere una delega, un'invocazione di skill e la lettura di una risorsa è obbligatorio: leggere uno SKILL.md non prova che la skill sia stata invocata dal programma. Le risorse tecniche dei tre adattamenti sono in `references/codex.md`, `references/claude-code.md` e `references/cursor.md` della stessa skill.
6. Se un agente o una skill necessari non sono riconosciuti o una chiamata fallisce, diagnostica nome, formato, percorso, permessi, versione e necessità di ricaricamento. Ripeti solo dopo una correzione pertinente. Non proseguire con il lavoro dipendente e non sostituire silenziosamente la delega con un ruolo recitato nella chat. Puoi completare attività indipendenti e documentare il blocco. Per ambienti non disponibili indica NON VERIFICATO.

La chat principale coordina. Ogni incarico include obiettivo, requisiti, file, permessi, skills necessarie, risultato atteso e destinatario; non presumere che un subagente abbia la cronologia. Conserva i limiti di sola lettura: in Codex il ruolo eredita i permessi della sessione, un campo sandbox_mode non garantisce isolamento separato. In Claude Code verifica che l'accesso a Skill sia consentito e precarica soltanto procedure sempre necessarie e attivabili. In Cursor usa solo campi documentati per quel programma. I modelli ereditano l'ambiente; la preferenza Codex di PromptAgent non diventa un modello Claude o Cursor.

`handoff` e `retro` restano su invocazione esplicita: `/handoff` e `/retro` in Claude Code/Cursor, `$handoff` e `$retro` nei client Codex che supportano tale sintassi, oppure il selettore disponibile. Se il programma richiede l'invocazione dell'utente, indica il comando e attendila; non aggirare il blocco leggendo ed eseguendo la procedura. Una consegna ordinaria usa TaskState.

Consegna quattro stati separati con evidenze: file generati, configurazioni controllate, elementi riconosciuti, chiamate effettivamente verificate. La presenza dei file e un --check riuscito non dimostrano esecuzione dei tre programmi.

## Destinazioni distinte

Per la fase 1 usa i comandi precedenti senza opzioni aggiuntive: installano `evaluation`, non AgentOptimizer. Per la fase 2 aggiungi `--phase optimizer` a ogni comando, usando come destinazione il repository canonico autorizzato: verrà installato `agent-optimizer`, non Evaluation. Entrambe le fasi preparano Codex, Claude Code e Cursor e le 14 skills.

Nel laboratorio PROMPT_AGENTI le configurazioni locali restano separate: usa il coordinatore e i ruoli di manutenzione già presenti, senza installare questo prodotto sopra il laboratorio. La valutazione del laboratorio resta statica. In altri repository canonici privi di quel laboratorio usa l’installazione optimizer richiesta.

Il benchmark autorizza le prove pertinenti entro scope e budget definiti; non autorizza deploy o modifiche ai prompt congelati. Concorda un budget prima di chiamate a pagamento se non è già stabilito. In assenza di runtime o misurazione salva la diagnosi con ANALISI_STATICA e metriche non misurate.

## 1. Nel progetto: orchestrazione e benchmark

Rendi accessibili anche il catalogo delle skills e le procedure aggiuntive attivate dal ruolo scelto, con le loro dipendenze. Carica soltanto i testi pertinenti; segnala quelli mancanti senza dichiararli applicati. Mantieni condizioni di confronto, provenienza dei dati e limiti dei ruoli nelle applicazioni delle skills.

Specifica da fornire: [EvaluationAgent_General.md](Agents/EvaluationAgent_General.md). Il risultato viene salvato in `agent-kit/reports/` o nella directory report già designata, fuori dalle cartelle di discovery degli agenti. Per una semplice raccolta di specifiche può restare nella loro cartella, se pertinente.

~~~text
Prima esegui la sequenza di installazione di questo PROMPTME e WORKFLOW.md nel progetto da valutare: anteprima, --apply, --check e riconoscimento nel programma disponibile. Installa il solo ruolo evaluation della fase predefinita e le 14 skills; conserva i prompt degli agenti sotto confronto. Agisci secondo EvaluationAgent_General.md e le skills fornite. Valuta gli agenti presenti in questo progetto e come lavorano in successione.

Individua dai file cartella degli agenti, istruzioni, ruoli, skills, configurazione reale, passaggi, test e log. Ricostruisci responsabilità, routing, input/output, limiti, ownership e handoff. Usa eventuali grafi come supporto e verifica le relazioni nelle fonti. Per un vault Obsidian segui la procedura Obsidian di project-graph-context: collega agenti, skills e handoff dai Markdown e confronta i contratti dichiarati con i passaggi osservati. Il progetto può usare qualsiasi linguaggio o stack.

Crea un benchmark rappresentativo e ripetibile, puntando a 20–50 casi in base ai dati e al budget disponibili. Distingui casi reali e sintetici; fissa criteri, errori critici e gates prima dei risultati. Congela versioni, dataset, rubrica e condizioni. Parti da un pilot di 3–5 casi e riutilizza gli strumenti di esecuzione e misura già presenti.

Se disponibili e autorizzati, orchestra gli agenti reali su copie isolate con lo stesso stato iniziale per ogni caso e variante. Misura successo, groundedness, chiamate, token, costo, latenza p50/p95, affidabilità, edit umani e qualità degli handoff. Registra run_id e step_id e separa costi della pipeline e dei valutatori. Confronta baseline e candidata sugli stessi casi, cambiando una cosa alla volta; conserva anche fallimenti e casi peggiorati.

Se manca una candidata, misura la baseline e proponi gli esperimenti prioritari. Se manca il runtime, salva diagnosi e piano con ANALISI_STATICA; un’eventuale esplorazione con ruoli nella stessa chat richiede una richiesta esplicita e va etichettata RUOLI_NELLA_CHAT; non sostituisce automaticamente il benchmark bloccato. Non inventare misure. Non correggere i prompt sotto confronto o alterare l'istanza attiva.

Salva BenchmarkReport.md in `agent-kit/reports/` o nella directory report già designata, fuori da `.codex/agents/`, `.claude/agents/` e `.cursor/agents/`, con il contratto agent-benchmark/v1 previsto dalla skill. Per una semplice raccolta di specifiche usa la loro cartella solo se pertinente e non utilizzata per discovery. Ogni finding deve collegare evidenza, caso/run/step, agente, requisito, problema, modifica proposta e prova successiva. Segnala metriche mancanti e restituisci PROMUOVI, NON PROMUOVERE o DATI INSUFFICIENTI secondo i gates. Il report deve essere trasferibile all'AgentOptimizer senza segreti o dati personali superflui.

Esegui il lavoro consentito senza chiedermi di avviare ogni fase. Usa scope e budget già autorizzati; chiedi soltanto un vincolo essenziale mancante. Concludi con il percorso del report, risultati osservati, limiti e interventi prioritari.
~~~

## 2. Nel repository canonico: revisione dei prompt

Specifica da fornire: [AgentOptimizerAgent_General.md](Agents/AgentOptimizerAgent_General.md). Aggiungi uno o più `BenchmarkReport.md` dei progetti, se disponibili.

~~~text
Nel repository canonico di destinazione rispetta prima le istruzioni locali. Se esiste un laboratorio con ruoli separati, passa la revisione al suo coordinatore senza installare prodotti sopra quei ruoli. Altrimenti installa il pack con --phase optimizer in tutti e tre i comandi (anteprima, --apply, --check), quindi verifica il riconoscimento di agent-optimizer nel programma disponibile prima di delegare. Agisci secondo AgentOptimizerAgent_General.md e le skills fornite, in modalità MIGLIORA. Analizza gli agenti e le skills di questo repository e integra i report di benchmark che ti fornisco.

Leggi prima specifiche, README, prompt di attivazione e convenzioni. Ricostruisci ruolo, attivazione, input/output, limiti e collaborazione. Nel vault Obsidian consulta i link dei Markdown secondo project-graph-context, distinguendo copie esportate, richiami di skills, contratti e consegne; ogni finding deve avere una fonte verificata e una prova successiva. Per i report verifica evidenze, modalità di esecuzione, versione dei prompt e personalizzazioni locali; collega gli agenti del progetto ai canonici senza presumere equivalenza dal nome. Se non ho un report, completa la diagnosi statica e indica il benchmark necessario.

Individua istruzioni ambigue, requisiti persi, analisi duplicate, routing errato e handoff incompleti. Distingui problemi dei prompt da difetti di runtime, dati o strumenti. Per ciascun finding indica evidenza, file/sezione, intervento preciso, rischio e test che ne misurerebbe l'effetto.

Preserva la versione originale confrontabile e applica le revisioni circoscritte autorizzate. Mantieni regole valide e responsabilità, spostando le procedure comuni nelle skills quando serve. Aggiorna i riferimenti e il README pertinenti. Mantieni semplice la struttura Agents/, Skills/, Prompts/, con ogni skill in nome-skill/SKILL.md e una sola fonte canonica per istruzione. Proponi nuovi ruoli soltanto per lacune documentate, con input/output, collaborazione e costo da verificare.

Salva OptimizationReport.md in `agent-kit/reports/` o nella directory report già designata dalle istruzioni locali, fuori da `.codex/agents/`, `.claude/agents/` e `.cursor/agents/`. In una semplice raccolta di specifiche può restare in Agents/ se pertinente e non usata per discovery. Collega finding F, cambiamento C, file/sezione, versione prima/dopo, controllo, prova successiva e stato. Le modifiche prive di confronto reale sono APPLICATO_DA_VALIDARE, con prestazioni DATI INSUFFICIENTI. Non alterare casi o rubriche per favorire una candidata. Quando l'ambiente lo consente, fai rivalutare la versione identificata da Evaluation sugli stessi casi; preserva la review finale in sola lettura.

Esegui le revisioni consentite senza chiedermi conferma per ogni passaggio già autorizzato. Non aggiornare automaticamente altri progetti. Consegna il percorso del report, modifiche, evidenze, limiti e il pacchetto minimo da rimandare al progetto per il prossimo benchmark.
~~~
