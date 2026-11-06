# Istruzioni per Claude

## Catalogo degli strumenti (repo GitHub)

Questo repo contiene un catalogo di plugin e strumenti esterni. I marketplace dei
plugin sono registrati in `.claude/settings.json`, ma **nessuno è attivo di
default**: si attivano solo quando servono davvero.

### Regola: suggerire all'avvio

All'inizio di ogni nuovo progetto o obiettivo, **prima di iniziare il lavoro**:

1. Leggi l'obiettivo dell'utente e confrontalo con la colonna "Quando usarlo".
2. Se uno o più strumenti sono utili, suggeriscili in una breve sezione
   "Strumenti consigliati": nome, perché serve per *questo* obiettivo, e il
   comando per attivarlo. Massimo 3 suggerimenti, i più pertinenti.
3. Se più strumenti si sovrappongono (es. i tre di design), consigliane uno e
   spiega in una riga perché quello.
4. Se nessuno è pertinente, non dire nulla: niente suggerimenti forzati.
5. Non attivare mai nulla da solo: aspetta la conferma dell'utente.

Rispondi in italiano.

### Catalogo — plugin di Claude Code

Si attivano con il comando nell'ultima colonna (in Claude Code, un comando per messaggio).

| Strumento | Cosa fa | Quando usarlo | Quando NON usarlo | Attivazione |
|---|---|---|---|---|
| **Ponytail** ([repo](https://github.com/DietrichGebert/ponytail)) | Modalità "senior dev pigro": codice minimo, riuso di ciò che esiste, senza togliere validazione, sicurezza e test. `/ponytail-review`, `/ponytail-audit`. | Scrivere o modificare codice; code review; audit di un repo esistente. | Lavori senza codice. | `/plugin install ponytail@ponytail` |
| **REA** ([repo](https://github.com/morluto/rea)) | Reverse engineering di app senza sorgente: binari nativi, JavaScript/Electron, .NET, siti web. | Capire come funziona una feature di un'app esistente per replicarla; analisi di eseguibili; ricerca di sicurezza autorizzata. | Quando hai già il sorgente. Per binari nativi serve Hopper/Ghidra/IDA. | `/plugin install rea@rea` |
| **Impeccable** ([repo](https://github.com/pbakaus/impeccable)) | Vocabolario di design per il frontend: 24 comandi (`polish`, `bolder`, `critique`, `audit`…) e controlli anti-"AI slop". | Rifinire o criticare l'interfaccia di un'app/sito **già esistente**; iterare sul look di componenti. | Partire da zero senza UI; backend. | `/plugin install impeccable@impeccable` |
| **Hallmark** ([repo](https://github.com/nutlope/hallmark)) | Skill di design che costruisce pagine web da 50 temi e le verifica nel browser contro i tic "fatti da AI". | Creare **da zero** una landing page, un sito vetrina, una pagina prodotto con un look curato e non generico. | App con molte schermate e logica; UI già definita. Il controllo nel browser richiede Chrome + `puppeteer-core`. | `/plugin install hallmark@hallmark` |
| **UI UX Pro Max** ([repo](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill)) | Database consultabile di stili, palette, font, grafici e linee guida UX; genera un design system su misura. | Definire un **design system** (colori, tipografia, componenti) per un'app o dashboard; scegliere stile e palette. | Testi o backend; ritocchi minori. | `/plugin install ui-ux-pro-max@ui-ux-pro-max-skill` |
| **Diagram Design** ([repo](https://github.com/cathrynlavery/diagram-design)) | Disegna diagrammi (45 tipi: architettura, sequenza, quadranti…) come un singolo file HTML+SVG, con i colori del tuo brand. | Schemi di architettura, flussi, matrici impatto/sforzo, organigrammi, diagrammi per presentazioni. | Grafici di dati numerici (usa uno strumento di grafici). | `/plugin install diagram-design@diagram-design` |
| **Humanizer** ([repo](https://github.com/blader/humanizer)) | Riscrive testi che "suonano da AI" in modo naturale, senza cambiarne il contenuto. | Post, email, articoli, annunci, documenti da pubblicare o inviare a persone. | Codice; testi tecnici dove conta la precisione letterale. Non serve a ingannare i rilevatori di AI. | `/plugin install humanizer@humanizer` |
| **last30days** ([repo](https://github.com/mvanhorn/last30days-skill)) | Ricerca su un tema negli ultimi 30 giorni su Reddit, X, YouTube, Hacker News, GitHub, Polymarket e altro, pesata per engagement. | Capire cosa si dice ora di un prodotto, trend, tecnologia o concorrente; ricerca di mercato rapida. | Fatti storici o stabili. Reddit/HN/GitHub/Polymarket gratis; altre fonti richiedono API key. | `/plugin install last30days@last30days-skill` |

### Catalogo — strumenti non-plugin

Non si attivano con `/plugin`: richiedono un'installazione a parte.

| Strumento | Cosa fa | Quando usarlo | Quando NON usarlo | Installazione |
|---|---|---|---|---|
| **Scrapling** ([repo](https://github.com/D4Vinci/Scrapling)) | Libreria Python + server MCP per web scraping: richieste HTTP, browser reali, parsing, crawler, esportazione in JSON/CSV/Markdown. | Estrarre dati strutturati da siti web; crawling di molte pagine; trasformare un sito in Markdown. | Siti con API ufficiale (usa quella); pagine singole leggibili con un semplice fetch. Rispettare termini d'uso e robots.txt. | `pip install "scrapling[ai]"`, `scrapling install` (browser), poi `claude mcp add scrapling -- scrapling mcp` |
| **Onyx** ([repo](https://github.com/onyx-dot-app/onyx)) | Piattaforma self-hosted (Docker) che indicizza le app del team (50+ connettori) per ricerca, chat e agenti con RAG. | Creare una **knowledge base aziendale**: far cercare/rispondere un'AI su documenti, Drive, Slack, wiki del team. | Progetti personali piccoli; non è un plugin per l'agente ma un servizio da ospitare su un server. | `curl -fsSL https://onyx.app/install_onyx.sh \| bash` su un server con Docker |

### Aggiungere un nuovo strumento

1. Se il repo contiene `.claude-plugin/marketplace.json`, aggiungi il marketplace
   in `.claude/settings.json` sotto `extraKnownMarketplaces` e una riga alla
   tabella dei plugin (nome plugin = `<plugin>@<marketplace>`).
2. Altrimenti aggiungi una riga alla tabella degli strumenti non-plugin.
