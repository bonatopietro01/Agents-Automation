# Starter pack

Ogni sottocartella è un pacchetto per uno scopo specifico.

| Pack | Scopo | Prompt da incollare |
|---|---|---|
| [Cover_letter_Pack](Cover_letter_Pack/README.md) | Configurare il progetto per candidature e cover letter personalizzate. | [PROMPTME.md](Cover_letter_Pack/PROMPTME.md) |
| [Full_stack_pack](Full_stack_pack/README.md) | Sviluppare e correggere un'app esistente, con PromptAgent e AIEngineer quando pertinenti. | [PROMPTME.md](Full_stack_pack/PROMPTME.md) |
| [App_starter_pack](App_starter_pack/README.md) | Avviare o organizzare un'app, nuova o esistente, con AppStarter e PromptAgent. | [PROMPTME.md](App_starter_pack/PROMPTME.md) |
| [Evaluation_pack](Evaluation_pack/README.md) | Misurare gli agenti nel progetto e usare le evidenze per migliorare i prompt canonici. | [PROMPTME.md](Evaluation_pack/PROMPTME.md) |

## Che cosa fa PROMPTME.md

Ogni PROMPTME contiene il prompt da incollare nella chat che lavora sul progetto di destinazione. App Starter, Full Stack ed Evaluation fanno eseguire il generatore incluso: controllano progetto e configurazioni esistenti, mostrano l'anteprima, applicano l'installazione, eseguono il controllo statico e verificano il riconoscimento nel programma disponibile. Cover Letter conserva il proprio flusso ChatGPT.

Rendi accessibile **l'intero pack**, incluso `pack.json` e tutte le risorse sotto Skills. Puoi copiarlo, per esempio, in `agent-kit/source/`; la sorgente deve restare distinta dai file generati. La sola copia non attiva agenti. Senza filesystem o Python 3.11+ la chat può preparare i passaggi necessari, ma non dichiarare installato il pacchetto. Il generatore non installa Python.

## Generatore locale per tre ambienti

Da ciascun pack software:

```text
python "<pack>/Skills/agent-configuration/scripts/install_agent_pack.py" --pack "<pack>" --project "<progetto>"
python "<pack>/Skills/agent-configuration/scripts/install_agent_pack.py" --pack "<pack>" --project "<progetto>" --apply
python "<pack>/Skills/agent-configuration/scripts/install_agent_pack.py" --pack "<pack>" --project "<progetto>" --check
```

Sostituisci i segnaposto con percorsi reali. Il comando senza opzioni mostra soltanto l'anteprima. L'installazione prepara **sempre tutti e tre** gli ambienti:

| Ambiente | Agenti generati | Skills |
|---|---|---|
| Codex | `.codex/agents/<nome>.toml` | `.agents/skills/<nome>/SKILL.md` e risorse |
| Claude Code | `.claude/agents/<nome>.md` con frontmatter | `.claude/skills/<nome>/SKILL.md` e risorse |
| Cursor | `.cursor/agents/<nome>.md` con frontmatter | Riusa `.agents/skills/` |

Cursor può scoprire anche le copie Claude: i contenuti dello stesso nome devono restare equivalenti; copie divergenti sono un conflitto. Tutte le 14 skills vengono incluse, ma si caricano solo quelle pertinenti. In Claude Code l'eventuale precaricamento `skills:` inserisce il corpo completo; le skills con invocazione manuale non vanno precaricate. Controlla che il ruolo possa accedere a Skill. Per handoff e retro PROMPTME spiega l'invocazione esplicita nel programma usato.

Il generatore registra fonti, nomi, percorsi e hash in `agent-kit/INSTALLATION.json`, installa `agent-kit/WORKFLOW.md` e integra sezioni delimitate in AGENTS.md e CLAUDE.md. Mantiene il testo esistente e aggiorna automaticamente solo file propri rimasti invariati. Risolve l'unione di più pack senza duplicare i ruoli condivisi; personalizzazioni e conflitti richiedono una risoluzione prima delle scritture. Le configurazioni installate sono autonome; per confrontarle con una versione sorgente usa --check con il relativo --pack.

Non crea configurazioni globali e non installa agenti nell'applicazione. Rifiuta l'installazione sopra il laboratorio locale o all'interno della sorgente del pack. La preferenza di modello Codex di PromptAgent rimane un'indicazione specifica; le configurazioni ereditano il modello dell'ambiente.

## Riconoscimento e diagnosi

PROMPTME e il riferimento `runtime-check.md` di agent-configuration richiedono la verifica nel programma disponibile. Se agenti o skills necessari mancano, controlla nome, formato, percorso, permessi, versione e caricamento; riprova dopo una correzione pertinente. Il lavoro dipendente resta bloccato, senza sostituzioni silenziose con ruoli applicati nella stessa chat. Una lettura di SKILL.md non equivale a un'invocazione nativa e una specifica non equivale a un subagente caricato.

Consegna sempre quattro stati separati: **file generati**, **configurazioni controllate**, **elementi riconosciuti**, **chiamate verificate**. Un --check riuscito dimostra coerenza statica. Gli ambienti non disponibili rimangono non verificati. In Codex i ruoli ereditano i permessi della sessione; `sandbox_mode` nel TOML del ruolo non crea una sandbox separata per il Reviewer.

## Composizione e nomi registrati

| Pack | Nomi registrati |
|---|---|
| App_starter_pack | `prompt-agent`, `app-starter`, `architect`, `backend`, `frontend`, `ai-engineer`, `reviewer` |
| Full_stack_pack | `prompt-agent`, `architect`, `backend`, `frontend`, `ai-engineer`, `reviewer` |
| Evaluation_pack, fase predefinita | `evaluation` nel progetto da valutare |
| Evaluation_pack, `--phase optimizer` | `agent-optimizer` nel repository canonico autorizzato |

Il coordinatore usa questi nomi attraverso gli strumenti effettivamente esposti; passa obiettivo, requisiti, file, permessi, skills e risultato atteso. PromptAgent si attiva per creare o migliorare prompt, non è una fase obbligatoria di ogni modifica. Evaluation e AgentOptimizer hanno destinazioni distinte: aggiungi --phase optimizer a tutti e tre i comandi solo per la fase nel repository canonico. Nel laboratorio locale di questa raccolta usa i ruoli di manutenzione già presenti e non installare i prodotti sopra di loro.

## Fonti canoniche

Agents, Skills e Prompts del repository restano canonici; i pack sono copie di distribuzione. Gli aggiornamenti non si propagano ai progetti esterni e devono preservarne le personalizzazioni. Il laboratorio locale resta separato dai prodotti condivisibili.

Riferimenti ufficiali verificati il 14 ottobre 2026: [Codex agenti](https://developers.openai.com/codex/subagents), [Codex skills](https://developers.openai.com/codex/skills), [Claude Code agenti](https://code.claude.com/docs/en/sub-agents), [Claude Code skills](https://code.claude.com/docs/en/skills), [Cursor agenti](https://cursor.com/docs/subagents), [Cursor skills](https://cursor.com/docs/skills).
