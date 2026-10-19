---
name: agent-design
description: Scrive o revisiona agenti, skills e prompt usando i requisiti confermati del laboratorio.
---

# agent-design

Per un agente definisci identità, trigger, input/output, responsabilità, permessi, limiti, skills condizionali, collaborazione e completamento. Per una skill definisci metodo riutilizzabile, name/description mirati, input, procedura, output e dipendenze reali; il name coincide con la cartella.

Conserva parti valide e correggi il difetto specifico. Evita procedure ripetute: una skill canonica contiene il metodo condiviso e gli agenti lo richiamano con una condizione precisa. Gli esempi spiegano il formato, non provano fatti sul progetto.

I prodotti generali devono essere portabili, senza dipendenze da .codex/, nomi lab_, dati personali, segreti o capacità inventate. Mantieni separate le fonti canoniche dalle copie esportate e dagli adattamenti locali.

PromptAgent prepara il prompt senza implementarlo; Designer modifica i file richiesti. Per richieste ampie conserva contesto comune e R-ID e suddividi per obiettivi/dipendenze. Usa [grilling](../grilling/SKILL.md) per decisioni aperte, [agent-graph-analysis](../agent-graph-analysis/SKILL.md) per collaborazioni e [scope-and-handoff](../scope-and-handoff/SKILL.md) per consegne. Controlla la copertura dei criteri e prepara evidenze per review.
