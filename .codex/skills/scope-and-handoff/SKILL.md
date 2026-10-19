---
name: scope-and-handoff
description: Conserva requisiti, owner e prove nei passaggi tra i quattro ruoli locali.
---

# scope-and-handoff

Usa un solo TaskState compatto: obiettivo, scope, fonti, R-ID, criteri, owner, decisioni, dipendenze, stati, prove e limiti. Un file ha un owner; Reviewer e valutatore non scrivono. Passa riferimenti e decisioni invece di transcript completi.

La consegna contiene mittente/destinatario, requisiti coperti/aperti, file e versioni, risultato, verifiche e prossimo passo. Stati: READY, DONE, BLOCKED, NOT_DONE, OUT_OF_SCOPE, NOT_APPLICABLE con motivo. Controlla che nessun requisito scompaia. Prepara un handoff a una nuova sessione soltanto quando richiesto; non inviare automaticamente messaggi ad altre chat. La chat principale effettua il routing e dichiara capacità/ruoli indisponibili.
