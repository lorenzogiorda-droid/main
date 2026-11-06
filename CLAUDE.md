# Istruzioni per Claude

## Catalogo degli strumenti (repo GitHub)

Questo repo contiene un catalogo di plugin e strumenti esterni. I loro marketplace
sono registrati in `.claude/settings.json`, ma **nessuno è attivo di default**:
vanno attivati solo quando servono davvero.

### Regola: suggerire all'avvio

All'inizio di ogni nuovo progetto o obiettivo, **prima di iniziare il lavoro**:

1. Leggi l'obiettivo dell'utente e confrontalo con la colonna "Quando usarlo".
2. Se uno o più strumenti sono utili, suggeriscili in una breve sezione
   "Strumenti consigliati": nome, perché serve per *questo* obiettivo, e il
   comando per attivarlo.
3. Se nessuno è pertinente, non dire nulla: niente suggerimenti forzati.
4. Non attivare mai nulla da solo: aspetta la conferma dell'utente.

Rispondi in italiano.

### Catalogo

| Strumento | Repo | Cosa fa | Quando usarlo | Quando NON usarlo | Attivazione (Claude Code) |
|---|---|---|---|---|---|
| **Ponytail** | [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail) | Modalità "senior dev pigro": codice minimo, riuso di ciò che esiste, senza togliere validazione, sicurezza e test. Comandi `/ponytail-review`, `/ponytail-audit`, `/ponytail-debt`. | Scrivere o modificare codice in un progetto software; code review; audit di un repo esistente; ridurre complessità e costi. | Lavori senza codice (documenti, analisi dati one-shot, testi). | `/plugin install ponytail@ponytail` |
| **REA** (Reverse Engineer Anything) | [morluto/rea](https://github.com/morluto/rea) | Server MCP + CLI per analizzare app senza sorgente: binari nativi, app JavaScript/Electron, .NET, siti web. | Capire come funziona una feature di un'app o sito esistente per replicarla; analizzare un eseguibile o un'app Electron; ricerca di sicurezza autorizzata. | Progetti dove hai già il codice sorgente; sviluppo normale. Per binari nativi serve Hopper/Ghidra/IDA installato. | `/plugin install rea@rea` (oppure `npx rea-agents setup`) |

### Aggiungere un nuovo strumento

1. Aggiungi il marketplace in `.claude/settings.json` sotto `extraKnownMarketplaces`
   (solo se il repo contiene `.claude-plugin/marketplace.json`).
2. Aggiungi una riga alla tabella qui sopra.
