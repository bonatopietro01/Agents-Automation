---
name: wiki-indexing
description: Usa per progettare o modificare estrazione, indicizzazione e retrieval di pagine, allegati o corpus della wiki.
---

# Indicizzazione e retrieval

Leggi l'inventario e il riepilogo esistente. Carica la [matrice dei formati](../../References/wiki-indexing-formats.md) solo per le famiglie pertinenti. Prima di scegliere parser, chunk e indice, chiarisci in round brevi e dipendenti solo ciò che manca. Registra le risposte una volta nel riepilogo del progetto.

1. **Scopo e accesso.** Quali fonti e derivati sono autorizzati per quali utenti? Chiarisci sensibilità, ACL (liste di controllo degli accessi), eventuali confini tra tenant, servizio esterno autorizzato o elaborazione locale, e chi decide revoche e cancellazioni. Raccogli query reali e risultati attesi, per esempio ricerca esatta, parafrasi, risposta con citazioni o calcolo su una tabella.
2. **Corpus e fedeltà.** Chiedi formati reali, conteggi, dimensioni tipiche e massime, lingue e percentuale di scansioni. Usa campioni autorizzati per capire tabelle, formule e valori salvati, colonne e righe nascoste, allegati, qualità OCR e granularità delle citazioni. Chiarisci eventuali vincoli per file protetti o malformati.
3. **Esercizio.** Concorda frequenza di aggiornamento, tempi di risposta, budget di parsing/OCR/embedding e gestione degli errori. Chiedi esempi difficili e un caso di accesso negato per ciascun confine rilevante. Proponi default motivati e mostra come cambiano se i campioni smentiscono le assunzioni. Procedi con l'implementazione solo quando scope e regole di accesso sono concordati.

## Scelta e contratto dei dati

- Parti dalla ricerca nativa full-text se servono parole, nomi, identificativi e filtri. Indicizza pagine, sezioni o record nei campi naturali del motore. Aggiungi vettori o ricerca ibrida quando query rappresentative mostrano un bisogno di similarità semantica o di recuperare passaggi per una risposta RAG. Usa dati strutturati o query controllate per totali, filtri e confronti esatti.
- Per retrieval semantico usa come default unità strutturali (titoli, sezioni, tabelle, record, slide). Preserva il percorso e il contesto minimo. Usa finestre a token solo per sezioni troppo lunghe, allineate a frasi o paragrafi quando possibile. Scegli dimensione e sovrapposizione dai risultati sui campioni e dai limiti effettivi del modello. Non attraversare confini di fonte o ACL.
- Ogni documento indicizzato o chunk conserva ID stabile, ID della fonte, revisione o hash, URI sicuro, posizione citabile, lingua, tipo, data, parser e versione/configurazione, versione del chunking, modello/versione embedding se usato, ACL effettiva e stato di estrazione. Risolvi le autorizzazioni lato server prima del retrieval e dei conteggi, snippet, citazioni o contesti RAG. Blocca il risultato se l'ACL è assente o incerta. Se il motore non applica il filtro prima del recupero, usa indici separati per confini di accesso o un motore compatibile.
- Mantieni un manifest con hash del contenuto, versione delle trasformazioni e revisione ACL separata. Riusa risultati invariati e aggiorna solo fonti o unità modificate. Su revoca o rimozione, blocca subito la consultazione e riconcilia chunk, indici derivati e cache. Su cambio parser o segmentazione, rigenera le unità interessate. Su cambio modello embedding rigenera i vettori compatibili in un indice separato e passa al nuovo indice dopo la verifica autorizzata. Conserva uno stato ripetibile per retry e cancellazione.

Per file Office con macro e varianti non verificate, applica la regola di supporto condizionale della matrice prima di scegliere il parser.

## Limiti operativi

Definisci un limite per ogni metrica applicabile della matrice. Usa come tetto di ingestione il minimo tra policy, prodotto, parser, servizio e budget nella stessa unità. Registra unità, fonte, versione/piano, owner, soglia, azione al superamento e criterio di revisione. Distingui tetto tecnico da default proposto e valida le ipotesi su campioni reali autorizzati. Rivedi i limiti quando cambiano volume, stack, costi o risultati.

Per superamenti, formato non supportato o esito incerto, scegli rifiuto, quarantena protetta, intervento manuale o estrazione alternativa autorizzata. Per estrazione parziale indica cosa manca e perché, preserva stato e provenienza, e mostra solo le parti ammesse e affidabili. Non far passare un documento incompleto per completo.

## Proposta e valutazione

Consegna una tabella formato → parser → unità → indice con limiti del progetto, modalità di esclusione e piano di aggiornamento. Confronta su poche query con fonte attesa una baseline full-text e l'alternativa eventualmente proposta. Verifica copertura dei campioni, precisione delle citazioni, correttezza su tabelle, accessi negati, revoche, freschezza, latenza e costo. Registra soglie concordate e risultati solo delle verifiche autorizzate.
