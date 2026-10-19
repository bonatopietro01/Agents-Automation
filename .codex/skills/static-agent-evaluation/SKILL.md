---
name: static-agent-evaluation
description: Confronta istruzioni di agenti e skills su casi e rubriche statiche, senza eseguire pipeline.
---

# static-agent-evaluation

Fissa domanda, scope, versioni, casi e rubriche prima del confronto. Usa casi comuni, incompleti e difficili; etichetta i casi sintetici. Ogni caso contiene ID, input, contesto consentito, stato iniziale, requisiti, rubric, fonti, controlli ed errori critici.

Valuta attivazione, responsabilità, limiti, dipendenze, input/output, ownership, requisiti, handoff e duplicazioni. Consulta [agent-graph-analysis](../agent-graph-analysis/SKILL.md) per le catene. Esiti: COPERTO_NELLA_SPECIFICA, LACUNA, NON_VERIFICABILE con file/sezione e motivo. Una copertura testuale non è task success.

Confronta baseline/candidata sugli stessi casi e mostra casi peggiorati. Report: versioni/hash, differenze, finding con gravità/fonte/caso, correzione mirata, limiti e controlli successivi. Groundedness degli output, calls/tokens/costo, latenza, affidabilità e human edits sono NON MISURATI. Nessun judge o pipeline reale. Valutatore read-only; la chat principale salva il report richiesto in .codex/reports/StaticEvaluation.md. Prestazioni: DATI INSUFFICIENTI.
