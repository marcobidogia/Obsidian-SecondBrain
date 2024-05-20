---
tags:
  - aws
---
### Overview
- Amazon Aurora è una tecnologia proprietaria di AWS, non open source
- Supporta i driver di Postgres e MySQL nativamente
- E’ “AWS Cloud optimized” e riceve un 5x delle performance per MySQL e un 3x per Postgress
- Lo spazio di storage di Aurora cresce di 10 GB per volta fino a 128TB
- Può avere fino a 15 Replicas e il processo di replica è più veloce rispetto a MySQL (sotto i 10 ms)
- Il failover è istantaneo infatti nasce nel cloud AWS quindi è nativamente High Available
- Aurora costa di più di RDS (20% in più) ma è più efficiente.

### Aurora High Availability e Scaling di lettura
- Aurora è speciale perché memorizza 6 copie del dato il 3 AZ ogni volta che esso viene cambiato
	- Questo serve per avere almeno 4 copie del dato su 6 per la scrittura nel caso ci siano problemi a raggiungere un AZ, e almeno 3 copie su 6 out per la scrittura
	- Comprende un processo di “self healing” del dato sulle repliche che permette il processo di rigenerazione di un dato che potrebbe essere danneggiato
	- non si affida a solo un volume ma è diviso in centinaia di volumi nel backend per evitare che nel caso di qualche guasto ci siano dei problemi
- Come gli altri processi Multi AZ anche aurora comprende solo un’istanza Master in cui avvengono le scritture e molte istanze replica dove vengono letti i dati
- Se il master non funziona, il processo di failover impiega meno di 30 secondi per scambiare l’istanza master non funzionante con una replica online.
- Supporta una cross region replication, quindi le repliche possono essere anche non nella stessa regione dell’istanza master. (1 M + 15 Replicas)

### Come funziona un Cluster Amazon Aurora (AZ e Replicas)
Vengono forniti due Endpoint per potersi collegare al proprio spazio di storage:
1. Writer Endpoint (Endpoint di scrittura) il quale provvederà a restituire il puntamento all'istanza Master, e a reindirizzare le richieste nel caso di failover.
2. Reader Endpoint (Endpoint di lettura) il quale bilancia il carico tra le repliche in lettura per poter rendere efficiente il processo di lettura. E’ possibile con questo gestire anche l’autoscaling delle istanze in lettura
I dati sono immagazzinati in uno spazio comune tra tutte le istanze del database, questo è diviso fra centinaia di volumi espansi a loro volta di 10 GB in 10 GB fino a 128 TB.
L’istanza Master di scrittura verrà impiegata per scrivere i dati sullo spazio comune e SOLO lei potrà accedere a questa funzionalità. Nel caso di problemi di questa istanza verrà eseguito il processo di failover prendendo dalle repliche.
Tutte le istanze replica saranno usate SOLO per la lettura dei dati, il loro carico viene bilanciato grazie all’endpoint di lettura. E’ possibile gestirne inoltre l’autoscaling.

### Principali Features
1. Failover automatico super rapido
2. Backup e Recovery (non con sistemi di backup classici ma con un metodo che può portare a fare diversi restore, ad esempio: oh devo rigenerare il punto di ieri alle 16.00. poi: ah cavolo avrei dovuto rigenerarlo alle 17.00, con questo metodo è possibile gestire questa situazione)
3. Sicurezza e isolamento dei dati
4. Industry compliance
5. Facile da scalare
6. Patch automatiche in tempo Zero
7. Monitoraggio avanzato
8. Routine di manutenzione gestite
9. Backtrack (sistema spiegato in punto 2)

### Sicurezza (RDS & Aurora)
- “At-rest” Encryption
	- Sono criptati sia master che repliche con AWS KMS. Necessita solo la definizione al momento del lancio di una nuova istanza
	- Il master decide se far cryptare le repliche o meno
	- Per cryptare e decryptare il database il processo passa attraverso gli snapshot
- “In-flight” encryption
	- TLS di default, con AWS TLS root per i certificati client
- IAM per l’accesso (IAM Roles)
- Security Group per il controllo network
- Non ha accessi SSH
- Possono essere creati log di accesso e salvati in cloudwatch per la lunga ritenzione

### RDS Proxy
Viene inserito all’interno della subnet privata del DB (e solo in questo modo per la sicurezza dei dati del DB); è utilizzato principalmente per ridurre il carico di lavoro nelle richieste di IN/OUT verso l’istanza RDS o Aurora.

Comprende i seguenti aspetti:
- Abilita le app all'accesso condiviso al database;
- Riduce lo stress sul database stesso in quanto minimizza le connessioni aperte.
- E’ Serverless, scalabile, highly available (comprende la tecnologia multi A-Z)
- Riduce il rischio di failover dei database del 66%;
- Supporta RDS e Aurora;
- Non necessita di nessun cambio di codice per essere implementato;
- Rafforza la sicurezza forzando l’autenticazione IAM con AWS Secrets Manager;
- Non può MAI essere pubblico (accesso solo tramite VPC).