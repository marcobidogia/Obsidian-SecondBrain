---
tags:
  - aws
  - sql
---
### Overview
(Pg. 137 AWS Certified Developer Slides )
RDS è l'acronimo di "Relational Database Service" e significa che è un servizio basato su database che utilizzano SQL come linguaggio di interrogazione. Permette di creare Database su motori quali:
- Postgres;
- MySQL;
- MariaDB;
- Oracle;
- Microsoft SQL Server;
- Aurora (generalmente poco usato in quanto ha una sezione dedicata all'interno della console di AWS essendo questo un software proprietario).

### Vantaggi nell'usare Amazon RDS Service invece di un EC2 con un database relaziona installato su di essa
(Pg. 138 AWS Certified Developer Slides )
RDS è un servizio gestito, in quanto tale, AWS ne fornisce tutti i servizi di aggiornamento, provisioning automatizzato, sistemi di patching e backup ed è inoltre in grado di gestirne un ripristino in un'area specifica chiamata: Point in Time Restore. Oltre a questi servizi è possibile anche disporre di dashboard di monitoraggio per visualizzare le prestazioni del database. Dispone inoltre di servizi di replica i quali permettono di gestire le [[RDS#repliche dei database|repliche dei database]] nel caso di una crescita pesante delle connessioni ai database. Per migliorare le prestazioni di lettura, è possibile configurare un multi AZ utile anche per il disaster recovery. Sono previste finestre di manutenzione per gli aggiornamenti e funzionalità di scaling pubblico, sia verticale, aumentando il tipo di istanza, sia orizzontale, aggiungendo repliche di lettura. Infine, lo storage è supportato da EBS, ovvero i volumi gp2 o io1.

> [!WARNING] NON SI PUO'
Utilizzare SSH per collegarsi ai propri database in quanto servizio gestito da AWS, però ogni operazione è possibile eseguirla dalle console di manutenzione

### Repliche dei database contro Multi AZ

RDS permette di gestire le cosiddette “Read Repliacs” che non sono altro che istanze aggiornate in modo ASINCRONO che permettono di gestire il traffico al database in modo più smart.
Un normale USE CASE è ad esempio:

Ho un applicazione che lavora in modo bilanciato con di RDS. Il carico di lavoro è bilanciato e le letture e le scritture vengono fatte da una singola istanza.
Ad un certo punto c’è la necessità di gestire un’applicazione di reportistica che va a “sovraccaricare” la macchina in produzione. Per evitare ciò sarà possibile creare una nuova istanza di RDS che serve per far leggere la nuova applicazione e non sovraccaricare l’istanza di produzione. Questa sarà aggiornata in modo asincrono quindi, la richiesta di scrittura che parte dalla produzione non aspetterà l’aggiornamento anche della replica per una risposta.

#### Costo delle repliche
Il costo delle istanze repliche è necessario solo quando le repliche vanno fuori dalla Region dell’istanza dove risiede l’istanza principale.
#### Disaster Recovery

Molto spesso viene utilizzato il metodo di Multi AZ per poter gestire eventi di failover in cui l’istanza principale non risulti più raggiungibile.
In questo caso viene creata un’istanza replica “Stand-by” in cui vengono immagazzinati i dati in modo sincrono.

> [!info]
Richiesta scrittura → Scrittura Istanza principale → Scrittura Istanza replica → Risposta alla scrittura
In questo caso, quando c’è il failover dell’istanza principale viene swappato il dns con l’istanza replica sempre aggiornata che mitigherà i problemi della mancata connessione alla principale.

### Possibili Engine
- Amazon Aurora
- MySQL
- MariaDB
- PostgreSQL
- Oracle
- Microsoft SQL Server

### Possibili argomenti d'esame
- The Read Replicas be setup as Multi AZ for Disaster Recovery (DR)
- Da singola AZ a multipla AZ del database cosa succede?
	- Zero Downtime operation (needs 1 click)
	- Cosa succede internamente:
		- Viene estratto uno snapshot del database principale
		- Viene creata una nuova istanza dallo snapshot in un’altra AZ
		- Vengono sincronizzati i due DB
		- La seconda istanza viene abilitato al funzionamento o di Standby o di Reader.

### Sicurezza RDS e Aurora
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