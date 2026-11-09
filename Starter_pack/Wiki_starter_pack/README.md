# Wiki Starter Pack

Guida un assistente con accesso ai file del progetto a progettare e realizzare una wiki pubblica, privata o ibrida. Funziona anche per una wiki esistente. Include un agente e procedure per progettazione, indicizzazione e manutenzione dei dati.

## Avvio

1. Copia l'intera cartella nel progetto oppure rendila accessibile nello stesso workspace.
2. Apri una chat nel progetto e incolla [PROMPTME.md](PROMPTME.md). Aggiungi l'obiettivo se lo conosci, per esempio «Voglio una wiki interna per onboarding e procedure, partendo dalla documentazione già nel repository».
3. Rispondi alle domande aperte. L'agente propone piattaforma, primo risultato utilizzabile e tappe successive con criteri di riuscita. Dopo la tua scelta applica le modifiche locali autorizzate.
4. Usa il riepilogo finale per decidere quali verifiche o operazioni esterne autorizzare e consegnare la manutenzione agli owner.

L'avvio è manuale e non richiede altri pack o un installer. L'assistente deve poter leggere il pack e il progetto. Servono permessi di scrittura per realizzare la wiki. Se mancano accessi, strumenti o autorizzazioni, l'agente indica il limite e consegna le parti che può completare.

## Contenuto

- [Wiki Builder](Agents/WikiBuilderAgent.md) definisce il flusso operativo e le autorizzazioni.
- [Progettazione](Skills/wiki-design/SKILL.md) guida domande, piattaforma, contenuti, accesso e semantica.
- [Manutenzione](Skills/wiki-operations/SKILL.md) guida backup, ripristino, migrazioni e monitoraggio in base allo stack.
- [Indicizzazione](Skills/wiki-indexing/SKILL.md) guida la scelta tra ricerca nativa e retrieval semantico, con una [matrice dei formati](References/wiki-indexing-formats.md) per estrazione e chunking.
- [Glossario di riferimento](References/wiki-glossary.md) raccoglie termini da adattare al progetto durante la progettazione.

La consegna tipica comprende pagine iniziali con fonti, struttura e navigazione, configurazione compatibile con il progetto e un manuale operativo per chi manterrà la wiki. Le parti applicabili dipendono dal percorso approvato.
