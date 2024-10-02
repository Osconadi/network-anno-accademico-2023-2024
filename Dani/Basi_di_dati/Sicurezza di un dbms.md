[[Controllo degli accessi]]
Obiettivi: segretezza, integrità, disponibilità

Tecniche:
- Autenticazione: basati principalmente su username e password
- Controllo dell'accesso : per ogni accesso ai dati si verifica che l'utente sia autorizzato (basato  sul dbms)
- Crittografia : cifrare dati

<h1> CONTROLLO ACCESSO </h1>

### Politiche di sicurezza

*Reference monitor* modulo dbms che si occupa di verificare se una richeista viene (autorizzata) soddisfatta o meno

Politiche per l'amministrazione della sicurezza
- Centralizzata: Un singolo utente (il database administrator) che gestisce l'intera base di dati
- Decentralizzata: Più soggetti sono responsabili del controllo di porzioni diverse della base di dati.
- Ownership: l'utente che crea un oggetto (proprietario) gestisce le autorizzazione sull'oggetto

Politiche per il controllo dell'accesso
Need to know (minimo privilegio) : restrittivo permette ad ogni utente l'accesso solo ai dati strettamente necessari per eseguire le proprie attività. Maggiore garanzia 
Maximized sharing (massimo condivisione) : consente agli utenti il massimo accesso alle informazioni nella base di dati mantenendo comunque informazioni riservate. Non serve proprio tanta protezione. 


### Comandi per la sicurezza

Grant
Revoke : solo privilegi che una persona ha grant


## Delega dei privilegi

#### I cataloghi SYSAUTH e SYSCOLAUTH


Il dizionario di una base di dati è una base di dati essa stessa


Revoca ricorsiva , timestamp di quando viene garantito l'accesso