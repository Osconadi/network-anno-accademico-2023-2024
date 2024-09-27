	Capitolo 12 di P.Atzeni e company

Le operazioni principali richieste pe ril controllo dell'affidabilità e del mantenimento corretto della transazioni sono il ***begin, commit, rollback***. Un altro componente importante sono il mantenimento del log delle operazioni compiute sul dbms e una memorai stabile, ovvero una memoria resistente ai guasti. 
#### Memoria stabile
Un piccolo accenno sulla memoria stabile è il fatto che questa viene spesso ottenuta tramite una duplicazione delle informazioni scritte su più dispositivi, come ad esempio un nastro e un disco su cui le informazioni sono speculari. Queste informazioni speculari con una scrittura attenta fa si che l'operazione di scrittura va a buon fine solo se scritta su entrambe le "copie".


### Il log
Se si perde il log è un evento catastrofico. 
Sul log vengono registrate tutte le transazione e opera praticamente come uno stack  dove l'ultima operazione eseguita è la più recente in ordine temporale.
![[Pasted image 20240612113921.png]]

Il Dump è una copia della base di dati che viene effetuata  in mutua esclusione con tutte le altre operazioni ed è solitamente un backup della base di dati effettuata in momenti di poco carico.
Il checkpoint invece è un momento in cui il log registra quali transazioni hanno completato il loro Commit (C) e quali altre sono ancora ins tato di attività.

Sul log operiamo attraverso le operazioni di :
- Begin(Transazione) che indica che sta venendo iniziata una transazione
- Update(T, O, BS, AS) che specifica la transazione che sta avenendo l'update su quale oggetto sta avvenendo e il **BEFORE STATE** e **AFTER STATE** di ognuna (lo stato del record rispettivamente prima e dopo l-aggiornamento). La Insert e il Delete sono casi particolari in cui si specifica o solo il BS o solo AS
- Commit e Abort che indicano sempre un identificativo della transazione e se questa va o meno a buon fine.

Per rifare o annullare delle operazioni abbiamo Undo e Redo che hanno la caratteristica di idempotenza, se ripetute queste avranno lo stesso risultato
Redo(Redo(A)) = Redo(A)


#### Regola di WAL e Commit-PRecedence
Per scrivere sul log abbiamo 3 schemi che per mantenere l'integrità devono rispettare la regola di Write Ahead Log. ergo si scrive prima sul log e poi sulla base di dati e del commit precedence in cui prima di effettuare il commit si deve scrivere il AS. Di fatto Il AS e BS vengono scritti contemporaneamente nel log prima di fare il commit (regola sempòificata).

I tre schemi che sono presentati mantengono queste 2 regole:
![[Pasted image 20240612115251.png]]
Nel caso a abbiamo che le scritture in database vengono eseguite prima del commit
Caso(b) le scritture in database avvengono dopo il commit
Caso(C) e piu comunemente usato le trascrizioni in database avvengono in un qualsiasi momento permettendo al buffer manager di decidere quando farle avvenire per una maggiore efficenza nella sua schedulazione.

### I guasti
Ovviamente sono da evitare ma è utile tenere a mente i due tipi di riavvio quando il sistema rivela uno di guasti.
Il sistema viene detto appunto fail-stop, se rilevato un guasto il sistema procede a fermarsi e riprendere un processo di boot da 0. Riavvio a freddo (cold-restart) e riavvio a caldo (warm restart)
rispettivamente guasti di sistema e di dispositivo.
![[Pasted image 20240612121656.png]]

### Anomalie in sistemi concorrenti
In sistemi in cui possono avvenire eventi di lettura e scrittura concorrenti  possono avvenire delle anomalie sulla consistenza del dato.
![[Pasted image 20240612121923.png]]

Noi affronteremo il concetto di gestione tramite timestamp, in  cui ogni transazione è associata un timestamp di quando questa avviene. 
Nei sistemi dbms ogni transazione è considerata AUTOCOMMIT, i comandi di commit/rollback eseguite manualmente indicano la fine della transazione corrente e permettono di iniziarne una nuova. In particolare il rollback può essere invocato automaticamente in caso di errore oppure manualmente dall'utente.
Inoltre devono essere mantenute alcune proprietà delle transazioni chiamte ACID
- ATOMICITY: le azioni devono essere atomiche, o avvengono o non avvengono (totali o nulle), le operazioni parziali vengono annullate e avviene un rollback.
- Consistency: la transazione deve mantenere i vincoli di integrità verificati, assumendo che nel DB questi vincoli siano sempre mantenuti. Possiamo verificare questi vincoli IMMEDIATE, immediatamente durante la transazione e eseguire un UNDO oppurtanatamente alla istruzione che li viola, oppure DEFERRED in cui si verificano i vincoli dopo la transazione e si fa un rollback in caso questi vengono violati.
- Isolation: L’isolamento garantisce che l’esecuzione di una transazione sia indipendente da altre transazioni in esecuzione simultanea. In altre parole, le transazioni non devono interferire tra loro e non devono vedere modifiche non ancora completate da altre transazioni.Le operazioni sono alternate in modo che l’esecuzione sia equivalente a qualche ordine sequenziale (seriale) delle transazioni (nozione di serializzabilità)
- Durability o persistancy, ottenuto tramite un log, assicura che le operazioni che arrivano al commit vengano registrati e che in caso di guasti prima della memorizzazione nel db possano essere recuperate.

	