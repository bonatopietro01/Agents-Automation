# Valuta gli agenti nel progetto e migliora i prompt canonici

Usa prima il prompt 1 nel progetto, poi il prompt 2 nel repository degli agenti. Copia soltanto il prompt della fase desiderata. Un file Markdown deve essere richiamato nella chat o configurato nell'ambiente; metterlo nella cartella non avvia l'agente.

Rendi accessibile l'intero [Evaluation_pack](../Starter_pack/Evaluation_pack/README.md) e applica la sequenza di [PROMPTME.md](../Starter_pack/Evaluation_pack/PROMPTME.md): anteprima, --apply, --check e riconoscimento nel programma disponibile. Python 3.11+ è un prerequisito; non installarlo automaticamente. Il pack prepara tutti e tre gli ambienti e le 14 skills complete. La fase predefinita installa evaluation nell'app; --phase optimizer installa agent-optimizer soltanto nel repository canonico autorizzato. Nel laboratorio locale di questa raccolta usa il coordinatore e i ruoli già presenti senza installare prodotti sopra di essi. Mantieni distinta analisi statica da riconoscimento e chiamate verificate.

## 1. Nel progetto: orchestrazione e benchmark

Rendi accessibili anche il catalogo delle skills e le procedure aggiuntive attivate dal ruolo scelto, con le loro dipendenze. Carica soltanto i testi pertinenti; segnala quelli mancanti senza dichiararli applicati. Mantieni condizioni di confronto, provenienza dei dati e limiti dei ruoli nelle applicazioni delle skills.

Specifica da fornire: [EvaluationAgent_General.md](../Agents/EvaluationAgent_General.md). Il risultato viene salvato in `agent-kit/reports/` o nella directory report già designata, fuori dalle cartelle di discovery degli agenti. Per una semplice raccolta di specifiche può restare nella loro cartella, se pertinente.

~~~text
Esegui prima la sequenza di installazione di Evaluation_pack/PROMPTME.md per la fase 1. Verifica il riconoscimento di evaluation; se manca diagnostica nome, percorso, formato, permessi, versione e ricaricamento prima del lavoro dipendente. Agisci secondo EvaluationAgent_General.md e le skills fornite. Valuta gli agenti presenti in questo progetto e come lavorano in successione.

Individua dai file cartella degli agenti, istruzioni, ruoli, skills, configurazione reale, passaggi, test e log. Ricostruisci responsabilità, routing, input/output, limiti, ownership e handoff. Usa eventuali grafi come supporto e verifica le relazioni nelle fonti. Per un vault Obsidian segui la procedura Obsidian di project-graph-context: collega agenti, skills e handoff dai Markdown e confronta i contratti dichiarati con i passaggi osservati. Il progetto può usare qualsiasi linguaggio o stack.

Crea un benchmark rappresentativo e ripetibile, puntando a 20–50 casi in base ai dati e al budget disponibili. Distingui casi reali e sintetici; fissa criteri, errori critici e gates prima dei risultati. Congela versioni, dataset, rubrica e condizioni. Parti da un pilot di 3–5 casi e riutilizza gli strumenti di esecuzione e misura già presenti.

Se disponibili e autorizzati, orchestra gli agenti reali su copie isolate con lo stesso stato iniziale per ogni caso e variante. Misura successo, groundedness, chiamate, token, costo, latenza p50/p95, affidabilità, edit umani e qualità degli handoff. Registra run_id e step_id e separa costi della pipeline e dei valutatori. Confronta baseline e candidata sugli stessi casi, cambiando una cosa alla volta; conserva anche fallimenti e casi peggiorati.

Se manca una candidata, misura la baseline e proponi gli esperimenti prioritari. Se manca il runtime, salva diagnosi e piano con ANALISI_STATICA; un’esplorazione con ruoli nella stessa chat richiede una richiesta esplicita e si etichetta RUOLI_NELLA_CHAT; non sostituisce automaticamente il benchmark bloccato. Non inventare misure. Non correggere i prompt sotto confronto o alterare l'istanza attiva.

Salva BenchmarkReport.md in `agent-kit/reports/` o nella directory report già designata, fuori da `.codex/agents/`, `.claude/agents/` e `.cursor/agents/`, con il contratto agent-benchmark/v1 previsto dalla skill. Per una semplice raccolta di specifiche usa la loro cartella solo se pertinente e non utilizzata per discovery. Ogni finding deve collegare evidenza, caso/run/step, agente, requisito, problema, modifica proposta e prova successiva. Segnala metriche mancanti e restituisci PROMUOVI, NON PROMUOVERE o DATI INSUFFICIENTI secondo i gates. Il report deve essere trasferibile all'AgentOptimizer senza segreti o dati personali superflui.

Esegui il lavoro consentito senza chiedermi di avviare ogni fase. Usa scope e budget già autorizzati; chiedi soltanto un vincolo essenziale mancante. Concludi con il percorso del report, risultati osservati, limiti e interventi prioritari.
~~~

## 2. Nel repository canonico: revisione dei prompt

Specifica da fornire: [AgentOptimizerAgent_General.md](../Agents/AgentOptimizerAgent_General.md). Aggiungi uno o più `BenchmarkReport.md` dei progetti, se disponibili.

~~~text
Rispetta le istruzioni locali del repository canonico: se dispone di un laboratorio separato usa il suo coordinatore senza installare prodotti sopra i suoi ruoli. Altrimenti applica la fase --phase optimizer di Evaluation_pack/PROMPTME.md e verifica agent-optimizer prima della delega. Agisci secondo AgentOptimizerAgent_General.md e le skills fornite, in modalità MIGLIORA. Analizza gli agenti e le skills di questo repository e integra i report di benchmark che ti fornisco.

Leggi prima specifiche, README, prompt di attivazione e convenzioni. Ricostruisci ruolo, attivazione, input/output, limiti e collaborazione. Nel vault Obsidian consulta i link dei Markdown secondo project-graph-context, distinguendo copie esportate, richiami di skills, contratti e consegne; ogni finding deve avere una fonte verificata e una prova successiva. Per i report verifica evidenze, modalità di esecuzione, versione dei prompt e personalizzazioni locali; collega gli agenti del progetto ai canonici senza presumere equivalenza dal nome. Se non ho un report, completa la diagnosi statica e indica il benchmark necessario.

Individua istruzioni ambigue, requisiti persi, analisi duplicate, routing errato e handoff incompleti. Distingui problemi dei prompt da difetti di runtime, dati o strumenti. Per ciascun finding indica evidenza, file/sezione, intervento preciso, rischio e test che ne misurerebbe l'effetto.

Preserva la versione originale confrontabile e applica le revisioni circoscritte autorizzate. Mantieni regole valide e responsabilità, spostando le procedure comuni nelle skills quando serve. Aggiorna i riferimenti e il README pertinenti. Mantieni semplice la struttura Agents/, Skills/, Prompts/, con ogni skill in nome-skill/SKILL.md e una sola fonte canonica per istruzione. Proponi nuovi ruoli soltanto per lacune documentate, con input/output, collaborazione e costo da verificare.

Salva OptimizationReport.md in `agent-kit/reports/` o nella directory report già designata dalle istruzioni locali, fuori da `.codex/agents/`, `.claude/agents/` e `.cursor/agents/`. In una semplice raccolta di specifiche può restare in Agents/ se pertinente e non usata per discovery. Collega finding F, cambiamento C, file/sezione, versione prima/dopo, controllo, prova successiva e stato. Le modifiche prive di confronto reale sono APPLICATO_DA_VALIDARE, con prestazioni DATI INSUFFICIENTI. Non alterare casi o rubriche per favorire una candidata. Quando l'ambiente lo consente, fai rivalutare la versione identificata da Evaluation sugli stessi casi; preserva la review finale in sola lettura.

Esegui le revisioni consentite senza chiedermi conferma per ogni passaggio già autorizzato. Non aggiornare automaticamente altri progetti. Consegna il percorso del report, modifiche, evidenze, limiti e il pacchetto minimo da rimandare al progetto per il prossimo benchmark.
~~~
