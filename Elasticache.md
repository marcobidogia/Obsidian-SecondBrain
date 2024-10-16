---
tags:
  - aws
---
### Overview
ElastiCache è un servizio di caching delle informazioni che riduce intensi workload di lettura dai propri database.
Lo spazio a disposizione può essere interrogato via Redis o Memcached.
I database Cache sono molto performanti e danno una bassissima latenza per le richieste, questi rendono le applicazioni stateless.
AWS ha in carico la manutenzione dei sistemi operativi, patching, ottimizzazioni, setup, monitoraggio e failover dei sistemi cache.

---
### Architecture

#### DB Cache
Molto spesso viene utilizzata un’architettura in cui l’applicazione va a richiedere i dati dalla cache invece di andare verso il DB di riferimento. Ovviamente quando manca il dato in cache verrà lanciata una query verso il DB e verrà ricevuto il risultato, prima di usarlo nell’applicazione è buona norma salvarlo nella cache per poter recuperarlo velocemente in seguito.

#### User Session
Un’altro esempio di architettura è quella per gestire la sessione utente.
in questo caso quando l’utente logga nell’applicazione, la prima volta scrive i propri dati sulla cache, ai collegamenti successivi verranno recuperati direttamente dalla cache.
Per le istanze Redis si potrà anche impostare una durata di ritenzione dei dati.

### Redis vs Memcached
Redis comprende i seguenti aspetti:
- E’ Multi AZ e comprende l’auto failover delle istanze.
- Può mantenere delle read replica per scalare le letture e migliorare la disponibilità.
- I dati sono persistenti.
- Le funzioni di Backup e di Restore sono assicurate.
- Supporta Set e Stored Set, un sistema a chiave per recuperare e salvare i dati.
Memcached comprende:
- Un sistema di multi node per partizionare i dati (sharding).
- NON comprende Replication.
- NON è persistente.
- NON comprende funzioni di Backup e Restore dei dati.
- Ha un architettura multi-thread.

### Caching implementation Considerations
- è sicuro fare il caching dei dati?
	per la maggior parte delle volte si, ma dipende sempre dal dato. questo potrebbe essere alcune volte “scaduto” e quindi non vale più la pena tenerlo
- il caching dei dati è ha effetto sui dati? da considerare i seguenti casi:
	- Il pattern dei dati, potrebbe aumentare le latenze se non fatto bene
	- Anti patterns, i dati cambiano troppo rapidamente e vengono frequentemente richiesti
- Come strutturati al meglio i dati?
	dipende dalla tipologia ma di base possiamo dire che devono essere almeno o chiave valore o in aggregazione di risultati.
- Che design pattern sono più appropriati?

### Architettura Lazy Loading/Cache-Aside/Lazy popolation
Considero un’applicazione di questo tipo:
Applicazione
→ Elasticache
→ Amazon RDS
L’applicazione in questione vuole recuperare un dato, per fare ciò eseguirà i seguenti passi:
1. Richiede il dato ad elasticache (CACHE HIT):
	1. Se presente, torna indietro il dato;
	2. Se non presente, passa a punto 2;
2. Manca il dato quindi la richiesta va all’istanza RDS che risponderà con il dato aggiornato
3. Una volta ricevuto il dato l’applicazione lo scarichera in Elasticache per renderlo disponibile in futuro

#### Pro
- Solo i dati richiesti vanno in cache.
- Il fallimento di uno dei nodi non è fatale, incrementa solo la latenza.

#### Contro
- Nel caso in cui i dati non siano presenti nella cache saranno necessarie 3 chiamate, quindi genera una latenza che per la user experience non è appropriata.
- Dati stantii, quindi i dati possono essere aggiornati in RDS ma se non c’è stata la cancellazione o l’aggiornamento in cache ci saranno dei dati obsoleti
Potrebbero esserci nell’esame domande per identificare questo tipo di strategia.

### Write Throught - Add or Update cache when database is updated
Prendendo lo stesso esempio di Architettura Lazy Loading/Cache-Aside/Lazy popolation nel in questo caso l’applicazione compierà i seguenti passi:
1. Tutte le richieste di lettura passano sempre per la cache, la quale è considerata sempre aggiornata.
2. Le richieste di scrittura seguiranno il seguente percorso:
	1. Aggiornamento su RDS
	2. Aggiornamento su Cache
Quindi i dati presenti su cache saranno una copia esatta di quelli presenti in RDS

#### Pro
- I dati presenti nella cache non saranno mai stantii, e le letture saranno super veloci
- Il fallimento di scrittura su cache consegue una perdita di tempo accettabile in quanto è in fase di scrittura (immaginando un utente, questo si aspetta che una richiesta di lettura sia sempre più rapida di una di scrittura)

#### Contro
- Maggiore spazio utilizzato nella cache di dati che non verranno mai letti
- Potrebbe verificarsi un disallineamento in fase di aggiunta di dati o di aggiornamento degli stessi, in questo caso ci si dovrà preoccupare di recuperare i dati con il metodo Architettura Lazy Loading/Cache-Aside/Lazy popolation.

### Cache Evictions and Time to live (TTL)
La cache ha uno spazio di memoria limitato quindi questi metodi servono per eliminare i dati per immagazzinarne di nuovi, ci sono 3 metodi:
1. Cancellare un dato esplicitamente sulla cache;
2. Nel caso in cui la cache sia piena cancellare i dati non usati di recente (LRU - List Recently Used);
3. Impostare il TTL ad esempio a 5 minuti, in questo caso, dopo 5 minuti i dati saranno cancellati dalla cache automaticamente.
Altre informazioni:
- Il TTL può essere utile per vari tipi di dati, commenti, streams, leaderboards.
- Il TTL può essere regolato da pochi secondi a ore o giorni.

### Use case
- Memorizzare i risultato delle query più comuni dai propri database per evitarne la ri-computazione.