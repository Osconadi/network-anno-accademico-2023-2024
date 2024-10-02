Fonte:  capitolo 1 del libro

Prima di accedere all'internet, qualsiasi dispotivo utilizza un tipo di accesso e ne esistono di diversi. La **LAN** può andare dal semplice network universitario a un raggrupamento di diverse LAN (ad esempio di una azienda). Tramite dei cavi, di rame o fibbre ottiche o altri supporti si connettono comunemente ad un **ISP** (internet service provider) che li collega poi al Global Internet.
Un'alternativa possono essere i cavi telefonici, una rete aziendale composta da diverse LAN oppure da connessioni wireless.

Grazie agli avanzamenti tecnologici nel campo della trasmissione dati, in particolare nella compressione di essi, tutti questi mezzi ora supportano diversi tipi  di media (prima ad esempio i cavi telefonici potevano solo mandare caratteri alfanumerici).

Una fattore da tenere in considerazione quando si parla di trasferimento di dati attraverso un network, sopratutto di dati sensibili è la questione della sicurezza.

### Applicazioni e terminologia del networking 
	Esattamente capitolo 1.2 del libro di testo

##### Tipi di dato e le loro caratteristiche
Esistono 3 tipi di *Text* : 
1) testo non formattato (unformatted text) 
2) testo formattato o richtext, un pdf un word con contenente anche eventuali immagini
3) ipertesto (hypertext) pagine web definite da link tra di loro, contenenti al loro interno testo formattato
Ognuno, seguendo il corso di Sistemi Operativi, in locale ha un modo diverso di essere trasferito e memorizzato. 

Le immagini si differenziano dalla loro provenienze, se sono immagini digitalizzate da supporti fisici oppure se prodotte al computer. Diventa irrilevante la loro provenienza poichè a livello di dato, queste vengono memorizzate in una matrice bidimensionale composta da pixel. 

	Ricordarsi che ad esempio un singolo pixel può essere espresso attraverso diversi canali, dagli 8 bit ai 24 e in su. Vedere il corso di Computer Graphics per approfondimenti.

La questione delle immagini prosegue per quanto riguarda i video. I video, oggi, sono principalmente una serie di immagini digitali in sequenza ognuno chiamato frame. Mandare questi frame manda anche il video essenzialmente. Per le televisioni, che funzionavano su supporto analogico, era importante prima digitalizzare su diversi formati (per diversi tipi di schermo) e poi riprodurre i frame digitalizzati  in sequenza. Questo viene detto raw bit rate di riproduzione e per un televisore digitale è di 162 mbs.


L'audio è un caso particolare. L'audio è generato in foram analogica, da un microfono che registra l'ampiezza dell'onda di un suono nel tempo. Bisogna perciò digitalizzarlo attraverso un convertitore analogico a digitale (ADC analog-to-digital converter) e poi per riprodurlo bisogna ritrasformarlo attraverso la controparte, ovvero un convertitore da digitale a a analogico (DAC). La qualità del tutto dipende dalla frequenza di "sampling" dell'onda.

Per fare una comparazione della quantità di dati il libro riporta l'esempio delle linee telefoniche, che produce (ai tempi) 64 kbps di bit rate, che messo in confronto al bit rate di un cd fisico di altà qualità produce più di 100 volte questa quantità, ovvero 705.6 kbps. Questo aumento quasi al doppio, a 1.4 mbps, per gli stereo. Qui arriva l'importanza di un algoritmo di compressione efficace.

#### Metodi di trasmissione
Due metodi intuitivi. O uno stream continuo di dati, uno streaming, oppure un trasferimento di dati in blocco. Nello streaming si considera il bitrate della sorgente e il bitrate del ricevente, a loro volta si può avere un bitrate costante o un bitrate variabile (VBR e CBR). Un esempio è quello di un video che può essere prodotto a bitrate costante ma ricevuto, dopo la compressione, a bit rate variabile.

La modalità a blocchi invece permetti di ricevere le informazioni prodotte ad un tempo non ben determinato. Mentre nello streaming è in "diretta", qui si possono ricevere ad esempio e-mail non a distanza di poco tempo. Un altro metodo del ricezione a blocchi è il downloading che è un ibrido, permette di trasmettere blocchi di dati e scaricarli a bit rate variabili, dove però il tempo di risposta da quando si richiede un pacchetto a quando si riceva debba essere non più di qualche secondo. Viene chiamato round trip delay (RTD)

![[Pasted image 20240926162244.png]]

#### Comunicazione e terminologia del networking