---
name: wiki-operations
description: Usa quando la wiki ha dati persistenti, una migrazione o un piano di manutenzione e ripristino.
---

# Manutenzione e ripristino

Parti da piattaforma, versione, ambiente, accessi, owner, inventario dei dati e autorizzazioni registrate. Chiedi quanta perdita di dati è accettabile e in quanto tempo il servizio deve essere ripristinato. Per una wiki a file, concentra la procedura su repository, media, configurazione e ricostruzione della pubblicazione.

1. Identifica la fonte primaria e distingui indici e cache ricostruibili. Mappa repository, database, media, configurazioni, metadati, segreti e permessi. Definisci chi possiede ciascuna componente e cosa copre l'eventuale provider. Applica privilegi minimi e separa gli account dell'applicazione, di manutenzione e di backup secondo necessità. [OWASP](https://devguide.owasp.org/en/04-design/02-web-app-checklist/03-secure-database-access/)
2. Definisci un backup coerente di dati, file e configurazione, con frequenza, conservazione, cifratura, accessi e avvisi per mancata esecuzione. Prepara un ripristino in ambiente isolato, usando versioni compatibili. Indica come controllare contenuti, allegati, permessi e ricerca dopo il recupero. Registra l'esito e il tempo soltanto quando il ripristino è stato provato. [Backup MediaWiki](https://www.mediawiki.org/wiki/Manual%3ABacking_up_a_wiki/en) · [Ripristino MediaWiki](https://www.mediawiki.org/wiki/Manual%3ARestoring_a_wiki_from_backup)
3. Per upgrade e migrazioni, controlla la compatibilità di motore, applicazione, plugin e schema. Prepara backup, prova su copia quando autorizzata, finestra, criteri per interrompere e piano di rollback o ripristino. Distingui trasformazioni reversibili da quelle che richiedono recupero da backup. [Aggiornamenti MediaWiki](https://www.mediawiki.org/wiki/Manual%3AUpgrading)
4. Monitora spazio, errori, latenze, connessioni, backup, job e stato dell'indicizzazione secondo la piattaforma. Definisci soglie, destinatari e azione attesa. Per un database, applica manutenzione, statistiche e gestione degli indici secondo motore, versione e misure effettive. Per esempio, con PostgreSQL valuta autovacuum e statistiche prima di proporre interventi manuali. [Manutenzione PostgreSQL](https://www.postgresql.org/docs/17/maintenance.html)

Prima di riaprire dopo un ripristino, riconcilia dalla fonte autorevole corrente i marcatori di cancellazione (tombstone), le revoche e le cancellazioni successive al backup. Riapplica permessi e retention a dati e derivati, riconcilia o ricostruisci cache e indici e blocca l'accesso fino al completamento della riconciliazione.

Consegna un manuale operativo con azione, ambiente, frequenza, owner, prerequisiti, criterio di riuscita ed evidenza. Includi revisione dei permessi, revisione editoriale, pagine obsolete, link interrotti, archiviazione ed export secondo necessità. Evidenzia i punti da provare e applica le autorizzazioni previste da Wiki Builder.
