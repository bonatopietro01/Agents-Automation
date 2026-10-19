---
name: grilling
description: Chiarisce le decisioni aperte prima di progettare un agente, una skill o il relativo prompt.
---

# grilling

Adattamento locale del metodo presente in Skills/grilling/SKILL.md. La procedura generale e la variante del laboratorio sono indipendenti.

Mappa un albero di decisioni: obiettivo, utenti, input/output, responsabilità, limiti, collaborazione, skills e criteri. Leggi i fatti dai file prima di chiedere. Chiedi alla persona soltanto decisioni o informazioni non ricavabili.

Lavora a round: domanda ciò le cui premesse sono già risolte, numera le domande, spiega le conseguenze e suggerisci una scelta motivata. Attendi le risposte prima delle domande dipendenti. Se il widget non appare, scrivi le domande direttamente in chat.

Aggiorna un solo TaskState con risposte e punti aperti. Non ripetere scelte risolte e non trasformare suggerimenti in requisiti confermati. Quando le decisioni necessarie sono risolte, riepilogale e attendi conferma prima di implementarle. Per una richiesta già determinata, procedi senza intervista obbligatoria. Output: requisiti confermati e questioni aperte. Un PRD si produce solo su richiesta.
