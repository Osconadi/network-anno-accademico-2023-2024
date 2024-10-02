Database management system è un software in grado di gestire collezione di dati che siano grandi, condivise e persistenti assicurando la loro affidabilitàa e privatezza. Una base di dati è una collezione di dati gestita da un DBMS.

(vedi anche [[DBMS - alternative]])

Su questi dati possiamo mettere vincoli e il DBMS garantisce che i dati siano coerenti con i vincoli.

In termini pratico è una connesione client server.
Il database è uno strumento di astrazione. Il DBMS è colui che si occupa di memorizzare a livello fisico secondo una sua determinata logica. E' trasparente al programmatore.

## Architettura a tre livelli

Livello Esterno (utente e applicazione) GUI

	indipendente logica dei dati

Livello Logico (schema logico)

	indipendente da come vengonono memorizzate in memoria fisica

Livello interno (fisico): storage 

### Mumbo jumbo dello schema funzionale
	vedi schifo slide
marginalmente importante sulla amministrazione di un database
Si toccherà principalmente il catalogo e il dizionario dei dati. Ovvero un'altra base di dati presente dentro il DBMS per catlogare i dati. Tramite il DDL si compila questo catalogo.

Con un DBMS si fanno le interrogazioni. Queste interrogazioni sono in programmazione dichiarativa è il DBMS che gestisce la richiesta tramite il linguaggio SQL. Si possono implementare in linguaggi esterni in vario modo. 


## Utenze di un DBMS
RICORDA: Su un dbms ci possono essere più database

DBA = amministratore database (di uno o più)
Hanno diversi funzionailità tra cui DDL, DML, DQL , DCL  (scaricare dati, modificare dati, fare query sui dati e concedere funzionalità ad altri utenti)

Il Superuser (in postgres si chiama POSTGRES) è il master di tutto, di ogni database e di quelli futuri.


DB user: utenti del database con privilegi specifici e limitati rispetto a un database.
Un utente puo ad esempio essere uno script esterno per interrogare i dati

Ci sono diversi livelli di expertise per gli User, devel user, occasional (non-expert), casual user.

## Accesso a un dbms

1) Client server comunication
2) Accesso sia da postazione locali o da remoto
3) GLi utenti utilizzano un software client che presentano : riga di comando, GUI e interfaccia web.