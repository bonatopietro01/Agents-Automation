---
name: agent-graph-analysis
description: Analizza le relazioni Markdown del vault Obsidian per migliorare collaborazione e skill routing.
---

# agent-graph-analysis

Input: scope canonico, file interessati e fonti disponibili. Distingui grafo dei prodotti generali e laboratorio locale. Escludi copie dei pack e report storici dall'inventario canonico, verificando i pack separatamente.

Leggi link Markdown e wikilink e la frase che descrive la relazione. Classifica usa_skill, dipende_da, consegna_a, concorda_con, review_di o riferimento. Conserva sorgente, destinazione, condizione e fonte. Un richiamo può essere indiretto; un ciclo owner-reviewer-owner è valido se ha un criterio d'uscita.

.obsidian/graph.json contiene impostazioni della vista, non nodi/archi. Ricostruisci il contesto dai Markdown e dichiara ANALISI_STATICA. Non dichiarare una consultazione visuale non eseguita. I TOML sono configurazioni; non presumere che Obsidian li rappresenti come nodi agente.

Cerca contratti incompatibili, requisiti persi, owner concorrenti, dipendenze senza risorse e procedure duplicate. Distingui lacune di navigazione da difetti del contratto. Aggiungi collegamenti solo alle relazioni documentate e autorizzate. Mermaid è una vista derivata. Non modificare le impostazioni .obsidian/. Output: relazione, evidenza, difetto/limite, intervento e caso statico.
