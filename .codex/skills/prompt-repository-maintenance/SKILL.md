---
name: prompt-repository-maintenance
description: Coordina esclusivamente il laboratorio PROMPT_AGENTI e preserva la separazione dai prodotti generali.
---

# prompt-repository-maintenance

Verifica la radice mediante README.md, Agents/, Skills/, Prompts/ e Starter_pack/. .codex/ contiene ruoli e procedure locali; le altre aree contengono prodotti e copie condivisibili. Escludi report storici dall'inventario degli agenti.

La chat principale coordina lab_prompt_agent, lab_agent_designer, lab_static_evaluator e lab_repository_reviewer. Solo il Designer modifica prodotti autorizzati; gli altri tre ruoli sono in sola lettura. La chat principale salva report in .codex/reports/ quando richiesti. ANALIZZA è senza scritture; MIGLIORA applica il task autorizzato; VALUTA è soltanto confronto statico.

Leggi solo le procedure pertinenti: [grilling](../grilling/SKILL.md) per decisioni aperte, [agent-design](../agent-design/SKILL.md) per istruzioni, [scope-and-handoff](../scope-and-handoff/SKILL.md) per consegne, [agent-graph-analysis](../agent-graph-analysis/SKILL.md) per relazioni, [static-agent-evaluation](../static-agent-evaluation/SKILL.md) per confronto e [export-pack-validation](../export-pack-validation/SKILL.md) per copie.

Prima di modificare conserva una baseline tramite Git, diff o snapshot verificato. Confronta copie/canonici e preserva personalizzazioni. Assegna owner per file, mantieni criteri, prove e limiti. Le modifiche passano al Reviewer quando disponibile; non dichiarare review indipendente se la stessa chat applica entrambi i ruoli. Non aggiornare progetti esterni. Usa i prodotti generali come fonti da analizzare, senza adottare le loro configurazioni come ruoli locali.
