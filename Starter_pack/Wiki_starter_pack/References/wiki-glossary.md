# Glossario di riferimento per progettare una wiki

Vocabolario iniziale per chiarire le decisioni di progetto. Adatta nomi, esempi e definizioni al dominio e alla piattaforma della wiki. Usa questo file come riferimento durante la progettazione. Per includere voci nella wiki, applica il normale processo editoriale e le autorizzazioni sulle fonti.

## Struttura e ricerca

| Termine | Significato nel progetto |
|---|---|
| Architettura dell'informazione | Organizzazione, denominazione e collegamento dei contenuti per aiutare il pubblico a trovarli e usarli. |
| Categoria | Raggruppamento di pagine per argomento o altro criterio. Una pagina può appartenere a più categorie. [MediaWiki](https://www.mediawiki.org/wiki/Help:Categories) |
| Modello di pagina | Struttura riutilizzabile con sezioni e campi attesi per un tipo di contenuto. |
| Indice di ricerca | Struttura derivata usata dal motore per trovare contenuti. Il progetto decide quali contenuti indicizzare e come rispettare i permessi. |
| Revisione e versione pubblicata | Una revisione registra lo stato di una pagina dopo una modifica. Una versione pubblicata mantiene un insieme di documenti per una specifica release. [Cronologia MediaWiki](https://www.mediawiki.org/wiki/Help:History) · [Versionamento Docusaurus](https://docusaurus.io/docs/versioning) |

## Vocabolario e semantica

| Termine | Significato nel progetto |
|---|---|
| Concetto ed etichetta | Il concetto rappresenta un'idea identificabile. L'etichetta è il nome con cui la si presenta. Si possono usare un'etichetta preferita e forme alternative. |
| Vocabolario controllato | Insieme governato di concetti e termini adottati per descrivere i contenuti in modo coerente. |
| Tassonomia | Classificazione che organizza i concetti in relazioni gerarchiche, per esempio più generale o più specifico. |
| Relazione associativa | Collegamento tra concetti pertinenti senza indicare che uno sia più generale dell'altro. |
| SKOS | Modello W3C per rappresentare e condividere concetti, etichette e relazioni di tassonomie e altri sistemi di organizzazione della conoscenza. |

Per concetti, etichette e relazioni, consulta la [raccomandazione W3C SKOS](https://www.w3.org/TR/skos-reference/).

## Governance e provenienza

| Termine | Significato nel progetto |
|---|---|
| Corpus autorizzato | Insieme di fonti approvate per un uso e un pubblico definiti. |
| Provenienza | Informazioni che permettono di risalire alle fonti, alle persone o ai processi che hanno prodotto o modificato un contenuto. |
| Responsabile editoriale | Persona o gruppo che decide come mantenere aggiornata una voce, correggerla o archiviarla. |
| Matrice dei permessi | Schema delle azioni consentite ai diversi gruppi su pagine, allegati e altre risorse. [Diritti utente MediaWiki](https://www.mediawiki.org/wiki/Manual:User_rights) |

Per approfondire la provenienza, consulta [W3C PROV Overview](https://www.w3.org/TR/prov-overview/).

## Backup e operazioni

| Termine | Significato nel progetto |
|---|---|
| Backup | Copia dei dati necessari per recuperare il servizio. Per una wiki può includere database, allegati e configurazione. [Backup MediaWiki](https://www.mediawiki.org/wiki/Manual:Backing_up_a_wiki/en) |
| Conservazione dei backup | Tempo per cui si tengono le copie prima di farle scadere o eliminarle. |
| Prova di ripristino | Recupero da una copia in ambiente isolato, seguito da controlli su pagine, allegati, permessi e altre funzioni essenziali. [Ripristino MediaWiki](https://www.mediawiki.org/wiki/Manual:Restoring_a_wiki_from_backup) |
| RPO | Obiettivo sul punto temporale a cui recuperare i dati. Esprime la perdita di dati tollerabile in termini di tempo. [NIST RPO](https://csrc.nist.gov/glossary/term/recovery_point_objective) |
| RTO | Obiettivo sul tempo entro cui ripristinare il servizio dopo un'interruzione. [NIST RTO](https://csrc.nist.gov/glossary/term/recovery_time_objective) |
| PITR | Recupero a un punto temporale scelto entro la finestra disponibile. PostgreSQL può farlo con un backup di base e la sequenza necessaria dei log WAL. [PostgreSQL PITR](https://www.postgresql.org/docs/current/continuous-archiving.html) |
