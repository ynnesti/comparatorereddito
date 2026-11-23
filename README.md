# comparatorereddito

Dove mi colloco? — Calcolatore di reddito globale

Uno strumento open source per confrontare il proprio reddito con la distribuzione mondiale, regionale e nazionale, basato sui dati ufficiali della Banca Mondiale.

Cosa fa

Lo strumento calcola, a partire dal reddito dichiarato dall'utente, tre percentili distinti:

Percentile nazionale — la posizione del reddito rispetto alla popolazione del paese selezionato
Percentile regionale — la posizione rispetto alla macroregione geografica di appartenenza secondo la classificazione della Banca Mondiale (es. Europa e Asia Centrale, Asia Meridionale, Africa Subsahariana)
Percentile globale — la posizione rispetto all'intera popolazione mondiale

Accanto ai percentili, vengono mostrati: il rapporto con la mediana nazionale, la soglia di povertà relativa (60% della mediana, standard UE), l'indice di Gini per la disuguaglianza del reddito, l'Indice di Sviluppo Umano (ISU/HDI) e il gruppo di reddito Banca Mondiale del paese.

Come funziona il calcolo
1. Conversione valutaria

Il reddito inserito (in qualsiasi valuta e periodo — mensile, annuale, settimanale o giornaliero) viene prima convertito in dollari USA usando tassi di cambio medi 2024.

2. Parità di Potere d'Acquisto (PPA / PPP)

Il valore in USD viene poi convertito in dollari internazionali 2021 a parità di potere d'acquisto (PPP 2021 int'l $), la stessa unità usata dalla Banca Mondiale nel database PIP. Questo passaggio è fondamentale: un euro in Italia compra meno di quanto farebbe in un paese a costi più bassi, quindi il confronto diretto ai tassi di mercato sarebbe distorto. I fattori PPP usati provengono dall'International Comparison Program (ICP) 2021 della Banca Mondiale.

3. Equivalenza familiare

Il reddito viene diviso per la dimensione equivalente del nucleo familiare, calcolata come: adulti + (figli × 0,5). Questo riflette la metodologia standard usata nel database PIP, che misura il benessere individuale all'interno del nucleo.

4. Interpolazione sui percentili

I dati PIP forniscono le soglie di reddito ai percentili p10, p20, p30, p40, p50, p60, p70, p80, p90 e p99. Per calcolare il percentile esatto corrispondente a un dato reddito, viene usata un'interpolazione lineare tra i due percentili adiacenti.

Fonti dei dati

Tutti i dati usati sono ad accesso libero e gratuito.

Distribuzione del reddito — World Bank PIP

Poverty and Inequality Platform (PIP) — pip.worldbank.org

La Banca Mondiale mette a disposizione un'API pubblica (api.worldbank.org/pip/v1/) che restituisce le distribuzioni del reddito per paese, per macroregione e per il mondo intero, espresse in dollari PPP 2021. I dati sono ricavati da indagini campionarie nazionali armonizzate (household surveys) e rappresentano l'anno più recente disponibile per ciascun paese (nella maggior parte dei casi 2019–2022).

I dati per le distribuzioni regionali e globali provengono dall'endpoint pip-grp con i parametri group_by=wb (regioni Banca Mondiale) e group_by=world.

Nota: l'Argentina non è inclusa per mancanza di dati PIP comparabili nel dataset 2021 (a causa di problemi statistici legati all'iperinflazione).

Indice di Gini — World Bank WDI

World Development Indicators — data.worldbank.org

L'indice di Gini misura la disuguaglianza nella distribuzione del reddito su una scala da 0 (uguaglianza perfetta) a 1 (massima disuguaglianza). I valori usati sono i più recenti disponibili per ciascun paese.

Indice di Sviluppo Umano — UNDP

Human Development Reports — hdr.undp.org

L'ISU (HDI) è un indice composito che misura salute, istruzione e tenore di vita. I valori usati sono quelli del rapporto 2023.

Fattori PPP — World Bank ICP 2021

International Comparison Program — www.worldbank.org/en/programs/icp

I fattori di conversione PPP indicano quanti dollari internazionali corrisponde un dollaro di mercato in ciascun paese. Per i paesi in cui il costo della vita è più basso degli Stati Uniti, il fattore è maggiore di 1; per i paesi più cari, è inferiore a 1.

Paesi inclusi (31)

Australia, Bangladesh, Brasile, Canada, Cina, Colombia, Egitto, Etiopia, Francia, Germania, Ghana, India, Indonesia, Italia, Giappone, Kenya, Messico, Paesi Bassi, Nigeria, Norvegia, Pakistan, Polonia, Russia, Corea del Sud, Sudafrica, Spagna, Svezia, Svizzera, Turchia, Regno Unito, Stati Uniti.

Lingue

Lo strumento è disponibile in italiano e inglese. Il selettore di lingua si trova in alto a destra nell'intestazione.

Limiti e avvertenze
I dati si basano su indagini campionarie: i percentili sono stime, non misurazioni esatte.
I tassi di cambio usati per la conversione valutaria sono medie annuali 2024 e non riflettono le fluttuazioni giornaliere.
Il reddito da confrontare è il reddito disponibile del nucleo familiare (al netto di tasse e contributi), non il reddito lordo. Inserire il lordo produce risultati sovrastimati.
La soglia di povertà relativa (60% della mediana nazionale in PPP) è uno standard convenzionale usato principalmente in ambito europeo e non coincide necessariamente con le soglie ufficiali nazionali.
Struttura del progetto
income-calculator/
└── index.html   # Applicazione completa (HTML + CSS + JS in un unico file)

Nessuna dipendenza esterna, nessun framework, nessun tracciamento. Il file pesa meno di 50 KB.

Licenza

I dati della Banca Mondiale e dell'UNDP sono rilasciati sotto licenza Creative Commons Attribution 4.0. Il codice di questo strumento è rilasciato sotto licenza MIT.

Crediti

Strumento realizzato da Albura con dati pubblici della Banca Mondiale (PIP, WDI, ICP) e dell'UNDP.
