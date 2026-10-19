---
name: export-pack-validation
description: Verifica copie e portabilità dei prodotti e l'assenza di dipendenze dal laboratorio locale.
---

# export-pack-validation

Ricava inventario dai file: attualmente nove agenti e quattordici skills generali. Escludi report dall'elenco dei ruoli. Confronta ogni copia inclusa nei pack con la fonte canonica prima di aggiornarla; preserva personalizzazioni divergenti.

Verifica file, risorse, frontmatter, link, input e workflow inclusi. Nessun prodotto o pack deve richiamare .codex/, ruoli lab_ o AGENTS.md locale. I cataloghi della radice possono spiegare la separazione, ma non sono dipendenze di esecuzione. Ogni pack contiene solo ciò che dichiara. Conserva il testo Cover Letter e la procedura di conteggio caratteri già prevista.

Riporta differenze, link mancanti e limiti. Designer corregge copie autorizzate; Reviewer e valutatore riportano findings senza scrivere. Non aggiornare automaticamente copie distribuite in progetti esterni.
