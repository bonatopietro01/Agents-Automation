# Laboratorio locale PROMPT_AGENTI

Questo progetto crea agenti e skills generali. I quattro ruoli di lavoro sono i TOML in `.codex/agents/`; `Agents/`, `Skills/`, `Prompts/` e `Starter_pack/` sono prodotti condivisibili.

Per lavorare sulla raccolta leggi [.codex/skills/prompt-repository-maintenance/SKILL.md](.codex/skills/prompt-repository-maintenance/SKILL.md), poi soltanto le skills locali pertinenti. Sono procedure richiamate esplicitamente: non presumere che siano nel catalogo automatico.

La chat principale coordina. Prompt o decisioni aperte: lab_prompt_agent con grilling quando serve. Implementazione autorizzata: lab_agent_designer. Confronto di istruzioni/grafo: lab_static_evaluator. Review delle modifiche: lab_repository_reviewer in sola lettura. La delega pertinente ai quattro ruoli locali è autorizzata; evita passaggi inutili. Se un ruolo non è disponibile, dichiara l'adattamento senza inventare indipendenza.

Valutazione esclusivamente statica; nessuna pipeline reale o misura operativa. Consulta le relazioni Markdown del grafo Obsidian e verifica condizioni nelle fonti. Non modificare il vault per una verifica.

Nessun prodotto o pack deve dipendere da .codex/, AGENTS.md locale o nomi lab_. Mantieni scope, requisiti e personalizzazioni. La chat principale salva i nuovi report locali in .codex/reports/ quando necessari. I report preesistenti in Agents/ restano storici e non sono ruoli.
