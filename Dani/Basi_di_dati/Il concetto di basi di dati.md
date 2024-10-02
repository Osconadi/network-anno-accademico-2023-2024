## Prima lezione

Basi di dati relazionale, lo scopo è capire come memorizzare una serie di dati. Diversi sistemi sia open source e non. (oracle)

Esistono anche basi di dati non relazionali. Nata da grandi volumi di dati  che non hanno troppi vantaggi dal relazionarli. Sistemi a grafi, documentali (not sql)

Esistono diverse teorie di basi di dati.


Algebra relazionale: linguaggio usato sulla "carta" per domandarsi sui dati.

E' importante saper progettare la base di dati e i loro [[Record]]

## Perchè usare le basi di dati

Bisogna dare un contesto interpretativo ai dati. Le basi di dati sono sempre relative ad un problema da affrontare. Esempio di memorizzare le vie: ad un servizio postale potrebbe tornare utile ricordare vari dati, dal civico al nome della via al cap ecc... mentre ad un uso più piccolo ad esempio basta solamente ricordarsi in una "colonna" la via e basta.

### Da dove vengono i dati
Come si costruisce un db?
I dati spesso arrivano da documenti.
**Dati non strutturati** : di solito testo (ma anche audio e immagini). I dati possono anche essere rappresentati in maniera strutturata ma non esplicita. (Esempio una ricetta). Un utente umano riuscirebbe ad infeerire un significato ai dati ma non un computer. I dati non sono orientati ad organizzarli.
Serviranno dei strumenti di parsing/manipolazione per usare questi dati in un db.

**Formato json** : semi strutturato. C'è una descrizione del dato che aiuta ad interpretare il dato, ma non ci sono dei vincoli precisi.

**Spreadsheet**: Ogni riga esprime un record ogni colonna una caratteristica. Questa è un modo coerente per le basi di dati. Questi sono dati **apparentemente strutturati**. 

L'operazione di join: mettere in relazione tabelle diverse che hanno delle corrispondenze

Per memorizzare i dati si usa un software il [[DBMS]]