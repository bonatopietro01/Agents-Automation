---
name: wiki-design
description: Usa per raccogliere requisiti, scegliere la piattaforma e progettare struttura, contenuti, accesso e ricerca di una wiki.
---

# Progettazione della wiki

Usa inventario del progetto e obiettivo come input. Prima leggi repository, documenti e risposte già raccolte. Mantieni un solo TaskState con fatti e fonti, decisioni confermate, proposte motivate, incognite, owner e criteri. Non riaprire una scelta risolta salvo evidenza nuova o cambio di scope.

Per conservare il TaskState tra chat, riusa un registro delle decisioni già presente nel progetto. Se manca, proponi un file nella documentazione del progetto, per esempio `docs/wiki-task-state.md`. Registra il percorso scelto nel riepilogo e aggiorna quel file quando la scrittura è autorizzata.

## Grilling adattivo

Nella prima sessione poni il primo gruppo breve di domande che sblocca una scelta. Nei round successivi segui le dipendenze e approfondisci lacune, blocchi e casi limite pertinenti. Usa i domini qui sotto come controllo di copertura, non come questionario fisso. Indica perché ogni risposta serve e marca il default suggerito come proposta. Se obiettivo, scope e valori sono già definiti, prosegui. Attendi le decisioni critiche prima di implementare.

Raggruppa solo domande indipendenti e attendi le risposte del round corrente prima di porre quelle che ne dipendono.

Per fonti, accessi e hosting, chiedi solo ciò che i file non chiariscono su giurisdizione, residenza dei dati, regioni ammesse, trasferimenti transfrontalieri e requisiti di privacy e conservazione, compresa la possibilità che dati o derivati escano dal confine autorizzato tramite parser, OCR, embedding, backup o log. Registra vincoli e owner nel TaskState.

Se una decisione dipende da termini ambigui o da un vocabolario condiviso, consulta il [glossario di riferimento](../../References/wiki-glossary.md) e adatta i termini al progetto.

1. **Scopo e utenti.** Individua lettori, autori, lingue e compiti prioritari. Ricava dai materiali o chiedi 3–5 domande reali, esempi di prime pagine utili e casi in cui la wiki dovrebbe astenersi dal rispondere. Definisci risultati osservabili per ciascun pubblico.
2. **Fonti e accessi.** Definisci profilo pubblico, privato o ibrido, gruppi, lettori, editor, revisori e amministratori. Chiarisci autenticazione, SSO, ACL, moderazione e cronologia. Valuta cosa può vedere un visitatore o un utente revocato via URL diretti, allegati, API, risultati, anteprime, cache ed export. Se l'isolamento non è garantito, separa aree o istanze o scegli un'alternativa. Chiarisci chi autorizza le fonti per uso e pubblico, gestisce licenze, sensibilità, attribuzione, conflitti, duplicati e ritiri. La possibilità di leggere un file non ne autorizza la ripubblicazione. Per le voci traccia fonte, data, licenza quando nota, owner e revisione. Distingui fatti, inferenze e lacune. [Manuale MediaWiki sull'accesso](https://www.mediawiki.org/wiki/Manual%3APreventing_access)
3. **Contenuti e integrazione.** Definisci tipi di pagina, titoli, identificatori, navigazione, link, template e contributi via browser o Git. Chiarisci posizione, hosting, stack, vincoli della piattaforma, database e integrazioni. Parti da categorie e link. Aggiungi entità, proprietà o relazioni quando una query concreta, un vocabolario condiviso o l'interoperabilità lo giustificano. Stabilisci esempi e vincoli. Identifica il bisogno di ricerca su corpus o allegati, estrazione o retrieval semantico e affida inventario dei formati, chunking e limiti a [wiki-indexing](../wiki-indexing/SKILL.md). [SKOS](https://www.w3.org/TR/skos-reference/) · [SHACL](https://www.w3.org/TR/shacl/)
4. **Esercizio.** Assegna responsabilità per wiki, database, aggiornamento, revisione e archiviazione delle pagine. Per una wiki esistente chiarisci cosa conservare, URL e allegati da mantenere, import/export e interruzione accettabile. Identifica esigenze di migrazione, backup, ripristino, retention, cancellazione e monitoraggio, inclusi guasti e responsabilità del provider. Applica [wiki-operations](../wiki-operations/SKILL.md) quando pertinente.
5. **Piano e accettazione.** Concorda budget, volumi, crescita e obiettivi di accessibilità. Definisci prima tappa, criteri di accettazione, rischi, casi limite da verificare e procedura di recupero. [WCAG 2.2](https://www.w3.org/TR/wcag/)

Per la ricerca tecnica online usa documentazione, repository, guide di migrazione e note di rilascio ufficiali. Verifica la compatibilità con le versioni del progetto. Per ciascuna conclusione importante registra fonte, versione o data di consultazione e conseguenza pratica. Esplicita eventuali dipendenze da estensioni e configurazioni. Se la ricerca non è disponibile, indica le informazioni da verificare. Chiedi un permesso distinto per usare il web come fonte delle voci e non trasmettere dati riservati.

Confronta al massimo tre approcci compatibili, per esempio Markdown nel repository, wiki collaborativa con editor web o integrazione nell'app. Raccomanda il percorso secondo sicurezza, lavoro editoriale, portabilità e manutenzione. Introduci un database dedicato solo se serve. Versiona le pubblicazioni quando il pubblico deve consultare più versioni. [Versionamento Docusaurus](https://docusaurus.io/docs/versioning)

Per l'opzione proposta indica posizione di sorgenti, allegati, database e indice, URL o percorso di accesso e integrazione con autenticazione, navigazione e aggiornamenti. Distingui funzioni iniziali e differite, compresi ricerca, cronologia, editoria e import/export. Per ogni componente aggiunto indica funzione, motivo, compatibilità, licenza, configurazione, permessi, costo ricorrente se noto e modalità di rimozione o sostituzione. Preferisci le risorse già presenti.

Consegna struttura, campione di pagine, matrice degli accessi, percorso di ricerca, strategia d'importazione e tappe con criteri. Collega ogni decisione ai requisiti del progetto.
