# Evaluation_pack

Confrontare pipeline di agenti in un progetto software e usare le evidenze per migliorare i prompt nel repository canonico. Include Evaluation e AgentOptimizer, con destinazioni e attivazioni distinte.

## Installazione e uso

1. Apri il progetto di destinazione in Codex, Claude Code o Cursor e rendi accessibile l'intero pack, comprese le risorse delle skills. Se lo copi nel progetto, usa una cartella sorgente distinta dai file generati, per esempio `agent-kit/source/`. Non rinominare o perdere il descrittore del pack.
2. Incolla [PROMPTME.md](PROMPTME.md) e aggiungi la richiesta concreta. Il prompt contiene i comandi del generatore Python 3.11+ e la sequenza anteprima → applicazione → controllo statico → riconoscimento nel programma disponibile.
3. Il generatore prepara **tutti e tre gli ambienti**, non solo quello attivo: agenti in `.codex/agents/`, `.claude/agents/`, `.cursor/agents/`; tutte le 14 skills complete in `.agents/skills/` e `.claude/skills/`. Le due copie devono restare equivalenti. Crea soltanto configurazioni del progetto.
4. Il manifest `agent-kit/INSTALLATION.json` registra fonti, nomi e hash. Le sezioni delimitate di AGENTS.md e CLAUDE.md preservano il testo esistente. Aggiornamenti automatici solo per file propri invariati: personalizzazioni e conflitti si risolvono prima delle scritture.
5. Segui [runtime-check.md](Skills/agent-configuration/references/runtime-check.md). Se un ruolo o una skill non viene riconosciuto, diagnostica nome, formato, percorso, permessi, versione e ricaricamento prima del lavoro dipendente. Non è previsto un ripiego silenzioso nella chat principale.
6. Il risultato distingue file generati, configurazioni controllate, elementi riconosciuti e chiamate verificate. Gli altri programmi restano non verificati. Se Python o l'accesso ai file mancano, dichiara il prerequisito e prepara i passaggi necessari senza installare software automaticamente.

Le configurazioni riguardano l'assistente di coding, non agenti AI eseguiti dall'applicazione. Vedi [installation.md](Skills/agent-configuration/references/installation.md) per dettagli del generatore. I modelli sono ereditati dall'ambiente e le skills condizionali si caricano solo quando servono; handoff e retro conservano l'invocazione esplicita.

La fase predefinita prepara il solo `evaluation` nel progetto software. Per la fase 2 usa `--phase optimizer` su anteprima/apply/check nel repository canonico autorizzato; non installare AgentOptimizer nell'app. Se il repository canonico ha già un laboratorio locale, usa il suo coordinatore senza sovrascriverne ruoli e skills.

## Contenuto e aggiornamenti

- [PROMPTME.md](PROMPTME.md): prompt separati per benchmark nel progetto e revisione dei prompt canonici.
- [WORKFLOW.md](WORKFLOW.md): ruoli, passaggi e limiti.
- `Agents/`: Evaluation per la fase nel progetto e AgentOptimizer per il repository canonico.
- [Skills/README.md](Skills/README.md): catalogo, trigger e dipendenze delle skills incluse. Applica solo quelle pertinenti; non precaricarle tutte se il runtime supporta l'uso condizionale.

Le fonti canoniche restano in `Agents/` e `Skills/` del repository PROMPT_AGENTI. I file nel pack sono copie derivate. Prima di ridistribuire aggiornamenti confronta le copie e conserva le personalizzazioni presenti nel progetto.
