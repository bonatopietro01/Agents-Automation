# Design: starter pack riutilizzabili per wiki e siti web

## Intento

Estendere il laboratorio PROMPT_AGENTI con due pack indipendenti: uno guida la progettazione, la creazione e la manutenzione di wiki di tipi diversi; l'altro copre la pianificazione, la realizzazione e la gestione completa di siti web. I pack sono strumenti riutilizzabili, non una wiki o un sito specifico. Prima di scegliere stack o piattaforma, gli agenti raccolgono le decisioni che cambiano struttura, permessi, dati e operazioni.

## Decisioni confermate

- Creare due pack separati, riusando i ruoli generali esistenti.
- La wiki deve supportare accesso pubblico, privato interno e misto per gruppi; il flusso chiede il profilo per ogni progetto.
- Il corpus autorizzato è la fonte iniziale. La ricerca web è ammessa solo se autorizzata nel progetto; i contenuti registrano provenienza e data, distinguono fatti, inferenze e lacune e rispettano licenze e riservatezza.
- Il modello semantico si attiva quando servono tipi, proprietà, relazioni, vocabolari controllati o interrogazioni tra entità; non è obbligatorio per ogni wiki.
- Il pack web copre siti informativi, documentazione, e-commerce e web app, scegliendo il flusso per ogni progetto.
- WebOps copre il ciclo operativo, ma ogni azione su dominio, hosting, account, produzione o dati reali richiede autorizzazione specifica.

## Approcci considerati

1. **Due pack separati con ruoli comuni riusati — scelto.** Mantiene responsabilità e installazioni pertinenti al progetto; condivide le policy generali e aggiunge soltanto i ruoli di dominio.
2. **Un pack combinato con modalità wiki e sito.** Riduce il numero di pack ma accoppia governance editoriale e operazioni web, caricando procedure non sempre pertinenti.
3. **Estensione di `Full_stack_pack`.** Riusa direttamente il pack più ampio, ma ne dilata lo scopo e rende meno chiaro quali ruoli servono per uno specifico progetto.

## Ruoli e ownership

Riutilizzare AppStarter per distinguere NEW/EXISTING/RUNNING e preparare scaffold autorizzati; Architect per decisioni trasversali e interfacce; Frontend per UI responsive e accessibilità implementata; Backend per servizi, dati e integrazioni; Reviewer per la review finale in sola lettura. AI Engineer è opzionale e si attiva solo per ricerca aumentata, RAG o assistenti. La chat principale resta l'unico coordinatore e conserva un TaskState con la copertura dei requisiti in un solo punto.

### Wiki pack

- **Wiki Information Architect:** possiede la discovery e il blueprint: utenti e compiti, ambito, profilo di accesso, pagine/tipi di contenuto, navigazione, vocabolario, relazioni semantiche quando richieste, governance, responsabilità editoriali e ciclo di revisione/archiviazione. Confronta piattaforme solo dopo aver raccolto i vincoli. Non scrive le voci né implementa la piattaforma.
- **Knowledge Curator:** prepara o aggiorna contenuti solo da fonti autorizzate; conserva citazioni/provenienza, data, licenza, owner e incertezza; propone collegamenti e segnala duplicati o contenuti da aggiornare. Non inventa fonti né cambia il modello semantico senza ownership esplicita.

### Website pack

- **Website Strategist:** raccoglie obiettivi, utenti, tipo di sito, azioni attese, contenuti, sitemap, percorsi e requisiti di ricerca/SEO e accessibilità. Consegna criteri e priorità, senza implementare UI o codice.
- **WebOps / Site Maintainer:** definisce e, quando richiesto e autorizzato, realizza rilasci e rollback, dominio/DNS/TLS, hosting, segreti e ambienti, backup e ripristino, monitoraggio, aggiornamenti e procedure d'incidente. Distingue istruzioni e piani da operazioni realmente eseguite; chiede autorizzazione separata per ogni azione esterna o in produzione.

Non aggiungere inizialmente ruoli separati per SEO, ricerca, designer grafico o content reviewer: le attività rientrano nei ruoli sopra o in Frontend/Reviewer. Si aggiungono solo se un caso d'uso reale non ha un owner chiaro.

## Skills specifiche

Creare procedure, non biografie o copie delle policy comuni:

- `wiki-information-architecture`: intake, struttura informativa, tassonomia, accesso e governance; se richiesto, un passaggio semantico leggero o strutturato.
- `knowledge-curation`: raccolta fonti, citazioni, licenze, qualità delle affermazioni, collegamenti e freschezza.
- `website-planning`: obiettivi, sitemap, percorsi, inventario dei contenuti, requisiti e criteri di accettazione.
- `web-operations`: runbook per rilascio/rollback, DNS/TLS, hosting, backup/ripristino, monitoraggio, incidenti e manutenzione con gate di autorizzazione.

Ogni `pack.json` elenca solo skills pertinenti e le dipendenze necessarie; usare `requirement-traceability`, `grilling`, `codebase-design`, `safe-refactor`, `investigate-first`, `handoff` e `retro` secondo i trigger già definiti, senza duplicarne il metodo. Handoff e retro restano espliciti. Le verifiche eseguibili seguono le autorizzazioni del TaskState: il pack non trasforma “verifica” in permesso generale per test, build, deploy o runtime.

## Flussi di discovery

La chat principale, non i singoli agenti in sequenza, raccoglie le risposte una volta e aggiorna TaskState. Per una wiki chiarisce: scopo e pubblico; accesso pubblico/interno/ibrido; corpus, autorità, sensibilità e licenze; contenuti e relazioni tra entità; necessità di query semantiche; lingue; editor, owner, revisione e archiviazione; criteri di successo. Per un sito chiarisce: tipo e stato NEW/EXISTING/RUNNING; pubblico e obiettivo; azioni principali; contenuti e lingue; design/brand esistente; SEO, accessibilità, privacy e sicurezza; stack e hosting consentiti; responsabilità e limiti operativi. Chiedere soltanto punti ancora aperti che cambiano una decisione, in round brevi con una scelta consigliata e il motivo.

## Piattaforme e semantica

Non fissare una piattaforma comune ai progetti. Valutare wiki collaborative con cronologia e governance, soluzioni basate su documenti/version control e sistemi di documentazione pubblicabile secondo accesso, contribuzione, ricerca, portabilità, costi e manutenzione. Per la semantica, usare una tassonomia leggera quando bastano concetti e relazioni; introdurre grafi, ontologie e validazione solo se query o interoperabilità li richiedono. Versionare la documentazione soltanto quando esistono versioni pubblicate da mantenere.

## Qualità e limiti

La wiki deve essere navigabile e collegata, verificabile nelle revisioni, governata per accesso e responsabilità e mantenuta contro obsolescenza. I siti devono trattare accessibilità, responsive design, sicurezza, prestazioni, contenuti utili e reperibilità come requisiti espliciti, oltre a deploy, rollback, backup, monitoraggio e aggiornamenti quando in scope. Nessun agente dichiara conformità o funzionamento senza l'evidenza autorizzata pertinente. Nessuna installazione o operazione su account reali è implicita.

## Riferimenti di ricerca consultati

- MediaWiki: [creare nuove pagine](https://www.mediawiki.org/wiki/Help:Starting_a_new_page), [categorie](https://www.mediawiki.org/wiki/Help:Categories), [cronologia](https://www.mediawiki.org/wiki/Help:History) e [permessi](https://www.mediawiki.org/wiki/Manual:User_rights).
- Semantica: [Semantic MediaWiki — proprietà e tipi](https://www.semantic-mediawiki.org/wiki/Help:Annotations), [W3C SKOS](https://www.w3.org/TR/skos-reference/) e [W3C SHACL](https://www.w3.org/TR/shacl/).
- Documentazione: [Docusaurus — Docs](https://docusaurus.io/docs/docs-introduction) e [versioning](https://docusaurus.io/docs/versioning), che evidenzia costo e complessità del versionamento.
- Web: [MDN — curriculum web](https://developer.mozilla.org/en-US/curriculum/about-curriculum/), [pubblicare un sito](https://developer.mozilla.org/en-US/docs/Learn_web_development/Getting_started/Your_first_website/Publishing_your_website) e [sicurezza](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Server-side/First_steps/Website_security); [WCAG 2.2](https://www.w3.org/TR/WCAG22/); [OWASP Top 10:2025](https://owasp.org/www-project-top-ten/); [Google Search Central — SEO Starter Guide](https://developers.google.com/search/docs/fundamentals/seo-starter-guide).

I riferimenti descrivono pratiche e capacità dei rispettivi standard/prodotti; non costituiscono una scelta della piattaforma dei pack né provano un'installazione o un comportamento runtime.
