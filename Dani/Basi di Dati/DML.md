DML ovvero Data manipolation language è una parte di SQL che lavorano sui dati, **NON** sulla struttura dei dati/tabelle

Nel DML rientrano:
- INSERT
- UPDATE
- DELETE


#### Insert, inserire un record
Ci sono alcune parole del linguaggi sql che sono attributi identificati dal linguaggi, come ad esempio **character** (che identifica un  carattere). Nel caso nella nostra base di dati abbiamo un attributo dal nome character dobbiamo identificarlo tra due apici quindi: "character" . Non solo questo serve ma anche per identificare eventuali altri alias di attributo.
Quando si usa il comando insert invece si usa il singolo apice ''

Quando si inserisce una nuova entry il dato non si troverà in fondo ma secondo un criterio di ordinamento, se presente, intrinseco di postgres (ad esempio).
**NON ESiSTE ORDINAMENTO**

Di base insert bisogna specificare tutti i valori da inserire, se volessimo inserire solo alcuni valori invece possiamo usare sempre insert ma specificando, subito dopo la tabella in cui inserire il dato, specificando i valori che vogliamo inserire

#### Delete, eliminare un record
Esempio:
delete from imdb.movie where id = 'asdka123'
la where specifica un parametro da valutare in questo caso si verifica uno ad uno l'id. CANCELLA LiNTERA ENTRY

Altro esempio
where year > '2010' ....
Qui sopra si esprime una espressione e possiamo anche esprimere una espressione complessa con predicati and not or ecc...

Se si esegue 
delete from imdb.movie;
è come dire delete... .... true ovvero elimina l'intera tabella. **PERICOLO**


#### Update, aggiornamento o modifica valore
update imdb.movie set year = '1974' where id = 'asdka123'
