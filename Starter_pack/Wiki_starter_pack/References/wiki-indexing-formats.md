# Matrice di estrazione e chunking

Usa queste regole come ipotesi da provare sui campioni autorizzati. Applica a ogni riga i metadati e le ACL definiti nella [skill di indicizzazione](../Skills/wiki-indexing/SKILL.md). La colonna «Citazione» aggiunge i riferimenti propri del formato.

| Formato | Unità e chunking | Citazione | Errori e limiti da gestire |
|---|---|---|---|
| Markdown, HTML | Sezione con percorso dei titoli. Mantieni liste, tabelle, blocchi di codice e testo alternativo come unità logiche. | Pagina, ancora, revisione. | Escludi menu e duplicati, non eseguire script né seguire link o include non autorizzati. Limita la dimensione dopo la normalizzazione. |
| PDF, scansioni | Estrai layout e testo per pagina e sezione. Usa OCR sulle pagine che ne hanno bisogno. Conserva tabelle, didascalie e intestazioni con il loro contesto. | Pagina, intervallo, coordinate se disponibili, metodo e confidenza OCR. | Controlla ordine di lettura, colonne e tabelle su più pagine. Segnala OCR incerto, limiti per pagine/pixel, pagine omesse, file protetti o malformati. |
| DOCX, ODT, RTF | Titolo, sezione, paragrafo e tabella. Mantieni note a piè di pagina associate al richiamo se autorizzate. | Percorso dei titoli, indice paragrafo o tabella. | Verifica supporto del parser per il formato, stili, revisioni, commenti e oggetti incorporati. Non eseguire macro. |
| XLSX, XLS, ODS | Leggi per foglio, tabella o intervallo. Raggruppa righe contigue con chiavi stabili e intestazioni ripetute per blocco. Mantieni nomi, tipi, unità, celle e relazioni tra colonne. | Workbook, foglio, tabella/intervallo, coordinate o chiavi riga. | Evita l'appiattimento indistinto. Distingui formula, valore salvato e valore visualizzato. Il valore salvato può essere assente o obsoleto. Non ricalcolare automaticamente né seguire link esterni. Concorda come trattare celle unite, righe e colonne filtrate o nascoste, fogli nascosti, formule e formati locali. |
| CSV, TSV | Record completi con schema e intestazioni. Raggruppa record compatibili e mantieni chiave, unità e tipi quando noti. | Nome dataset, riga logica o chiave, colonne. | Verifica separatore, codifica, quoting, valori con nuove righe, intestazioni mancanti e righe fuori schema. Imposta limiti per riga e dimensione. |
| PPTX | Una slide con titolo e testo come unità, con note e tabelle se autorizzate. Suddividi slide molto dense in gruppi coerenti. | Numero e titolo slide, origine tra testo, nota o OCR. | Segnala slide nascoste, note riservate, ordine di lettura incerto e oggetti incorporati. |
| JSON, XML | Record o sottostruttura per percorso con campi selezionati. Conserva gli identificatori e un riferimento al padre. | ID, JSON Pointer o percorso XML equivalente. | Valida schema, profondità e dimensioni. Disabilita entità XML esterne e recuperi di rete. Escludi campi sensibili fuori scope. |
| EML, MSG | Messaggio per unità, con allegati gestiti secondo formato e autorizzazioni. Separa corpo, cronologia citata e firme. | ID del messaggio, data, allegato, segmento del corpo. | Controlla metadati personali, thread duplicati, codifica e allegati protetti. Non abilitare risorse remote. |
| Immagini | OCR per regione o didascalia descrittiva autorizzata. Conserva l'immagine come fonte se previsto. | File, frame o regione, metodo e confidenza OCR. | Controlla risoluzione, rotazione e lingua. Rimuovi metadati sensibili dai derivati. Distingui ciò che è letto da ciò che è inferito. |
| Archivi | Estrai ogni membro ammesso e applica le regole del suo formato. | ID archivio e percorso interno del membro. | Limita profondità, numero di membri, espansione, byte e tempo. Blocca percorsi fuori destinazione, link simbolici e membri inattesi. |
| Audio, video | Trascrizione per segmento temporale e cambio argomento. Considera OCR di frame solo se utile e autorizzato. | Intervallo temporale, traccia, lingua e confidenza quando disponibile. | Limita durata, dimensione e costo. Segnala audio mancante, diarizzazione incerta, parole dubbie e restrizioni sui partecipanti. |
| Codice | File e simbolo come unità. Mantieni firma, documentazione pertinente e riferimenti al contesto. | Percorso, commit, intervallo di righe, simbolo. | Ignora vendor, binari e generati fuori scope. Escludi segreti. Non eseguire il codice per indicizzarlo. |
| Export database | Usa schema e record autorizzati, con chiavi e confini di accesso. Se servono aggregazioni usa query controllate. | Dataset, versione export, tabella, chiave riga. | Non eseguire dump SQL. Limita tabelle, righe, colonne e join. Proteggi chiavi sensibili e mantieni permessi fino al record. |

Per `.docm`, `.xlsm` e `.pptm` applica la riga della famiglia Office corrispondente solo se il parser supporta esplicitamente la variante. Non eseguire macro né seguire collegamenti o query esterni. Segnala che VBA e oggetti incorporati potrebbero non essere estratti. Per `.xlsb` e altre varianti non verificate, verifica su un campione autorizzato oppure escludi il formato o usa un'estrazione alternativa autorizzata.

## Soglie da compilare per progetto

| Ambito | Limiti e regole da definire |
|---|---|
| Documento e OCR | Byte per file, pagine per documento, pixel per immagine e qualità minima OCR per lingua o campione. |
| Fogli e tabelle | Fogli, righe e celle per file o intervallo. Regole su formule, valori salvati, celle unite, dati nascosti e filtri. |
| CSV e TSV | Byte per riga logica, righe e colonne per file, tipi, campi obbligatori e trattamento delle righe fuori schema. |
| Archivi | Byte estratti totali e per membro, rapporto di espansione, profondità e numero di membri. Applica anche i limiti dei formati contenuti. |
| JSON e XML | Byte, profondità e numero di record o nodi. |
| Audio e video | Durata, byte, tracce, frame e volume di trascrizione. |
| Indice e query | Token per chunk e query, sovrapposizione, chunk per fonte, dimensioni e numero di vettori, candidati recuperati e latenza. |
| Esecuzione | Timeout, memoria, costi per unità e per periodo, tempo massimo prima che modifiche, revoche o cancellazioni risultino effettive. |

Per ciascuna soglia usa il criterio della [skill](../Skills/wiki-indexing/SKILL.md) e registra l'esito quando interviene. Imposta limiti di decompressione, tempo e memoria prima di elaborare dati non fidati.

## Esempi documentati dei fornitori

Consultazione del 2026-11-07. Sono dati dei servizi o modelli indicati. Controlla versione, piano e regione applicabili prima di usarli come criteri del progetto.

- **Azure AI Search.** Come punto di partenza per finestre fisse, Microsoft propone 512 token con 128 di sovrapposizione. Nei limiti degli indexer, la dimensione massima del file sorgente varia tra livelli, per esempio 16 MB per Free/Basic, 128 MB per S1 e 256 MB per S2/S3. La modalità CSV `delimitedText` ha un buffer massimo di 10 MB per riga. [Chunking](https://learn.microsoft.com/en-us/azure/search/vector-search-how-to-chunk-documents) · [Limiti per livello](https://learn.microsoft.com/en-us/azure/search/search-limits-quotas-capacity)
- **OpenAI File Search / vector store.** La configurazione predefinita è 800 token con 400 di sovrapposizione. Per la configurazione statica, la dimensione ammessa è 100–4096 token e la sovrapposizione va tenuta entro metà della dimensione. [Documentazione Retrieval](https://developers.openai.com/api/docs/guides/retrieval#chunking)
- **Azure Document Intelligence.** I limiti documentati di analisi sono 500 MB in S0 e 4 MB in F0. Per PDF/TIFF sono indicate fino a 2.000 pagine, o le prime due in F0. Nel conteggio, ogni foglio Excel e ogni slide PowerPoint vale una pagina. Per gli input Office i modelli Read e Layout non analizzano le immagini incorporate o collegate. [Quote e limiti](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/service-limits) · [Requisiti di input](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/train/custom-model?view=doc-intel-4.0.0)
- **Microsoft 365, elaborazione di documenti non strutturati.** Il modello non esegue le formule XLS/XLSX e tronca il testo analizzato oltre 64.000 caratteri. Verifica separatamente come il parser del progetto tratta formule e valori salvati. [Requisiti del modello](https://learn.microsoft.com/en-us/microsoft-365/documentprocessing/requirements-and-limitations?view=o365-worldwide)
- **Microsoft Graph Excel REST.** L'API Excel supporta le cartelle di lavoro Office Open XML e non il formato binario XLS. [Documentazione dell'API](https://learn.microsoft.com/en-us/graph/api/resources/excel?view=graph-rest-1.0)
