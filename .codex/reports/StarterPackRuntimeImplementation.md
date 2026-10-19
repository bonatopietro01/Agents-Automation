# Starter pack per Codex, Claude Code e Cursor

Data: 14 ottobre 2026. Scope: generatore locale, nove specifiche, quattordici skills, tre pack software e relativi punti d'ingresso. Nessuna installazione in app reali e nessuna pipeline LLM eseguita.

## Requisiti e risultato

| ID | Requisito | Implementazione ed evidenza |
|---|---|---|
| R1 | Tre ambienti con generatore locale | `Skills/agent-configuration/scripts/install_agent_pack.py`, Python 3.11+, sola libreria standard; preview, apply, check. |
| R2 | Identità e dipendenze esplicite | `references/roles.json` e tre `pack.json`; skill complete nei due percorsi, riscrittura dei link degli agenti e controllo delle dipendenze incluse. |
| R3 | Preservare file e personalizzazioni | Manifest con percorsi, fonti e SHA-256; ownership, sezioni delimitate, preflight, snapshot prima delle scritture, staging e ripristino su errori intercettati. |
| R4 | Chiamate corrette | Contratto comune in requirement-traceability; ID in nove agenti; handoff/retro espliciti; guida delle skills distingue i tre programmi. |
| R5 | Pack pronti e isolamento | PROMPTME/WORKFLOW/README dei tre pack e prompt generici; Evaluation fase project e optimizer separate; Cover Letter e laboratorio indipendenti. |
| R6 | Prove e limiti | Suite temporanea deterministica, controllo link/copie, review indipendente e procedura runtime-check per i progetti di destinazione. |

## File coinvolti

- Canonici: nove `Agents/*_General.md`.
- Skills modificate: agent-configuration, requirement-traceability, handoff, retro, writing-for-agents/SKILL-MECHANICS.md, pipeline-benchmark. Tutti i quattordici SKILL.md sono stati letti; le altre procedure restano valide e non sono state riscritte senza motivo.
- Nuove risorse di agent-configuration: due script, roles.json e cinque guide (installation, codex, claude-code, cursor, runtime-check).
- Distribuzione: tre pack.json e copie equivalenti dei canonici nei tre pack software; documentazione dei pack, README principale/cataloghi e tre prompt di ingresso aggiornati.
- Cover Letter escluso dalle modifiche. Nessuna modifica ai ruoli/skills di manutenzione locali o alle impostazioni Obsidian.

## Decisioni

- I modelli sono ereditati. La preferenza PromptAgent resta nelle sole istruzioni Codex derivate; nessun modello OpenAI è impostato nella configurazione Claude/Cursor.
- Codex non riceve sandbox_mode: i permessi provengono dalla sessione. Claude limita PromptAgent/Architect/Reviewer a Read, Glob, Grep e Skill; Cursor usa readonly. Questi adattamenti non dimostrano il rispetto operativo dei limiti.
- Nessun preload automatico delle skills. Handoff e retro mantengono entrambe le politiche specifiche dei programmi.
- Il workflow installato è un coordinamento comune generato, non una copia byte per byte dei WORKFLOW dei pack. AGENTS.md e CLAUDE.md ricevono un puntatore delimitato, preservando il contenuto esterno alla sezione.
- I report runtime e i loro dati vanno fuori discovery, normalmente in agent-kit/reports. Nelle semplici raccolte di specifiche resta ammessa la collocazione accanto ai prompt.
- Più pack condividono file equivalenti. Versioni divergenti e rimozioni richiedono riconciliazione/migrazione esplicita; non viene introdotto un aggiornamento forzato o un disinstallatore.
- Lo scanner controlla il progetto; eventuali configurazioni globali, cartelle antenate, plugin e cataloghi remoti si verificano nel programma.

## Conservazione della base

Lo snapshot completo iniziale era stato creato nella cartella temporanea della sandbox (181 file), ma quella cartella non è risultata accessibile nelle chiamate successive. Non viene presentato come archivio recuperabile.

Prima della sincronizzazione, le copie preesistenti di agenti e skills nei pack sono state confrontate fra loro: nessuna divergenza. Sono conservate nell'archivio `StarterPackBeforeSync-2026-10-14.zip` accanto a questo report (SHA-256 `A89D9CA3D464F74E3C0FEDB122840D9B85AFDFCD37BB26CD7912A0F31F59E670`). L'archivio conserva la base originale di agenti e skills e Cover Letter; la documentazione dei pack era già aggiornata. Non è quindi una baseline integrale dei README prima del lavoro.

## Skills locali applicate e collaborazione

| Skill locale | Procedura applicata | Risultato |
|---|---|---|
| `.codex/skills/prompt-repository-maintenance/SKILL.md` | Separazione laboratorio/prodotti, inventario, conservazione base | Scope dei file e archivio locale, nessun runtime installato nel laboratorio. |
| `.codex/skills/agent-design/SKILL.md` | Conservazione responsabilità, trigger, I/O e permessi | Nomi registrati, contratto condiviso e adattamenti specifici. |
| `.codex/skills/scope-and-handoff/SKILL.md` | Owner disgiunti per generatore, specifiche e documentazione | Consegne esplicite e sincronizzazione unica dalla chat principale. |
| `.codex/skills/agent-graph-analysis/SKILL.md` | Link e frasi: usa_skill, dipende_da, consegna_a, review_di | Dipendenze risolte negli output; ruoli assenti espliciti; nessuna modifica alla vista Obsidian. |
| `.codex/skills/export-pack-validation/SKILL.md` | Confronto copie, dipendenze e isolamento | Hash equivalenti e Cover Letter preservato. |
| `.codex/skills/static-agent-evaluation/SKILL.md` | Casi di configurazione, attivazione e consegna | Copertura statica; qualità/costi/token/latenza NON MISURATI. |

Usate inoltre skill-creator per lo script deterministico e OpenAI Docs per le fonti ufficiali. Nessun grilling: le scelte erano già confermate. I collaboratori separati hanno applicato i contenuti dei ruoli locali Designer/Reviewer; non è stata dichiarata una chiamata nativa ai nomi TOML lab_*.

## Review e correzioni

| Finding | Correzione | Evidenza |
|---|---|---|
| Risorsa aggiunta a una sola copia skill non rilevata | Controllo dell'inventario completo, non solo file nel manifest | Caso extra.txt preservato e installazione bloccata. |
| Variazione utente fra prepare e apply | InstallPlan conserva bytes osservati; riconfronto prima di staging e sostituzioni | Test dedicato che crea una regola utente dopo prepare. |
| Report interpretati come configurazioni agente | Percorsi di report fuori dalle directory di discovery | Canonici, skill, workflow e prompt allineati. |
| Check dopo più pack cambiava ordine delle fonti | Ordinamento stabile delle fonti nel manifest | Full Stack + App Starter + Evaluation, otto ruoli senza AgentOptimizer. |

Reviewer separato: correzioni approvate entro scope statico; nessun nuovo difetto materiale individuato nel ricontrollo. Le esecuzioni finali della suite appartengono al coordinatore, non al Reviewer.

## Verifiche

Risultato finale della suite: **24/24 superati** con Python 3.12.14 e `--temp-root .installer-test-temp` sotto il workspace. Copertura: anteprima senza scritture, prima installazione, idempotenza, percorsi Windows con spazi e caratteri accentati, aggiornamento di file propri, personalizzazioni e conflitti, ID duplicati, risorse mancanti, metadati manual-only, copie skills divergenti/risorse extra, più pack reali nello stesso progetto, fase optimizer separata, report esclusi, variazioni fra anteprima e applicazione, rollback su errore simulato e protezione del laboratorio. Nessuna prova LLM o chiamata ai programmi.

Controllo documentale: 556 link locali esaminati nelle aree dei prodotti, zero destinazioni mancanti; 126 copie di file canonici confrontate, zero differenze. Due file Cover_letter_Pack uguali alla copia archiviata. Questi conteggi escludono i report storici dalle specifiche attive.

La prima esecuzione dei test nella directory temporanea del sistema è fallita per permessi WinError 5 prima delle prove del generatore. Le prove successive usano cartelle temporanee isolate sotto una radice scrivibile del workspace tramite --temp-root. Nessuna correzione dei permessi di sistema.

## Limiti e verifica successiva

File generati e controlli statici sono verificati in cartelle di prova. Riconoscimento e chiamate effettive in Codex, Claude Code e Cursor: **NON VERIFICATI**. Seguire `Skills/agent-configuration/references/runtime-check.md` nel progetto destinatario. Non sono stati misurati task success, groundedness, latenza, token, costo o interventi umani.

Il validatore non è un parser YAML universale, non controlla URL remoti o frammenti Markdown e non prova il comportamento delle istruzioni. Il rollback copre errori intercettati, non spegnimenti/arresti forzati. Lo stato dei target viene ricontrollato prima dello staging e prima delle sostituzioni; per progetti modificati contemporaneamente ripetere il preflight se emerge un conflitto.

Fonti ufficiali consultate: [Codex subagents](https://developers.openai.com/codex/subagents), [Codex skills](https://developers.openai.com/codex/skills), [Claude subagents](https://code.claude.com/docs/en/sub-agents), [Claude skills](https://code.claude.com/docs/en/skills), [Cursor subagents](https://cursor.com/docs/subagents), [Cursor skills](https://cursor.com/docs/skills).
