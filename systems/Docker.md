---
tags:
  - systems
---
# Cos'è Docker   
  
Nella visione più "antiquata" i programmi dovevano essere compatibili con il sistema operativo sul quale funzionavano, le librerie di cui necessitavano e l'infrastruttura hardware del pc ospitante. Tutto ciò prevedeva un enorme perdita di tempo nel mantenere stabile cercando di non "pestare i piedi" a nessun processo. Dopo ciò è nata la necessità di avere una tecnologia che permetta di spezzettare le varie funzionalità in piccoli contenitori.   
Vista questa necessità è nato ***Docker*** . Questa tecnologia consente di gestire una macchina come se fosse un insieme di contenitori chiamati **Containers** e di renderli indipendenti l'uno dall'altro con il sistema operativo e hardware sottostante.   
   
# Containers   
  
I containers sono la più piccola parte di docker, ogni container effettivamente è una "macchina virtuale" che con in proprio hardware virtuale.   
Docker però non ha inventato container, infatti questi esistevano già in passato ma erano di difficile utilizzo. Docker ha reso questi molto più semplici da usare.   
Esistono vari tipi di container LXC, LXD, LXCFS, docker utilizza i contenitori LXC.   
Per comprendere a pieno il funzionamento di container e docker è necessario ragionare sul sistema operativo.   
Docker utilizza il Kernel per basare i propri container, se il kernel è quello di Linux ecco che potrà eseguire solo sistemi Linux based, e non ad esempio Windows server. Se docker viene montato su Windows esso portà montare anche Linux in quanto verrà montato su una macchina virtuale con linux e da li verrà avviato.   
   
## Note   
Molte aziende hanno i propri docker che sono semplicemente raggiungibili da un Public Docker Registry o Dockerhub.   
   
# Images   
 --- 
Le immagini di Docker sono il template a cui si basa il container per funzionare, per crearle sarà necessario:   
1. Creare un file chiamato "Dockerfile" con all'interno le istruzioni utili al container per funzionare;   
	1. Recarsi alla cartella con il cmd e da li avviare il comando    
```
docker init
```
A seguito del comando sarà creato un Dockerfile in cui ci saranno tutte le informazioni per avviare il container.   
2. lanciare il comando    
```
docker build <cartella di destinazione, "." per la cartella corrente> -f <Dockerfile> -t <nome dell'applicazione come tag>
```
   
## Differenza fra CMD e ENTRYPOINT in dockerfile   
 --- 
In un `Dockerfile`, `CMD` e `ENTRYPOINT` sono entrambe istruzioni che specificano quale comando deve essere eseguito all'avvio del container. Tuttavia, hanno scopi leggermente diversi e interagiscono tra loro in modi specifici.   

### CMD   

- **Scopo Principale**: `CMD` specifica il comando di default da eseguire quando il container viene avviato. Se non viene specificato un `ENTRYPOINT`, il `CMD` viene eseguito direttamente.   
- **Sovrascrivibile**: Il comando fornito da `CMD` può essere sovrascritto specificando un comando differente alla fine del comando `docker run`.   
- **Uso Tipico**: Viene usato per definire argomenti di default che possono essere sovrascritti dall'utente quando il container viene eseguito.   
   
### ENTRYPOINT   

- **Scopo Principale**: `ENTRYPOINT` specifica un comando che sarà eseguito ogni volta che il container viene avviato. A differenza di `CMD`, non è inteso per essere sovrascritto con opzioni al comando `docker run` (anche se può essere sovrascritto con l'opzione `--entrypoint`).   
- Interazione con `**CMD**`: Quando sia `ENTRYPOINT` che `CMD` sono specificati, `CMD` fornisce argomenti aggiuntivi che vengono passati all' `ENTRYPOINT`.   
- **Uso Tipico**: Viene usato per impostare il container come un eseguibile specifico. `ENTRYPOINT` permette al container di essere eseguito come un comando, e `CMD` può fornire argomenti di default per quel comando.   
   
### Esempi   

- Solo `**CMD**`:   
   
```
dockerfileCopy code
CMD ["python", "app.py"]

```
Questo avvia `app.py` usando Python quando il container viene eseguito, ma può essere sovrascritto specificando un altro comando alla fine del comando `docker run`.   
- Solo `**ENTRYPOINT**`:   
   
```
dockerfileCopy code
ENTRYPOINT ["python", "app.py"]

```
Questo fa sì che `app.py` venga sempre eseguito con Python all'avvio del container, e non può essere facilmente sovrascritto senza usare l'opzione `--entrypoint`.   
- `ENTRYPOINT` e `**CMD**`:   
   
```
dockerfileCopy code
ENTRYPOINT ["python"]
CMD ["app.py"]

```
In questo caso, `python` è il comando che viene eseguito all'avvio del container, e `app.py` è l'argomento di default passato a Python. Gli utenti possono sovrascrivere `app.py` con un altro script specificandolo alla fine del comando `docker run`, ma `python` rimarrà il comando principale eseguito.   
La scelta tra `CMD` e `ENTRYPOINT` dipende dalla modalità in cui si desidera che il container venga utilizzato e se si prevede che gli utenti necessitino di sovrascrivere il comando di avvio del container   
   
## Envinroment variables   
  
Passare ad un container delle informazioni da fuori può essere una pratica vincente per evitare di dover riscrivere molte volte il codice dell'applicazione stessa.   
Per questo Docker contiene una funzionalità chiamata Envinroment variables, queste sono delle variabili le quali verranno passate all'applicazione come variabili di sistema.   
```
docker run -e <NOME DELLA VARIABILE>=<VALORE> <image>
```
Il comando soprastante avvia il container con la variabile di sistema con il valore desiderato.   
Per accedere alle variabili in uso dal container in funzione è possibile avviare il comando:   
```
docker inspect <id container>
```
e ne verranno visualizzate le variabili nella sezione Config.   
   
# Docker compose   
  
Docker compose è il comando che compone nello stesso host diversi containers insieme per renderli un applicazione completa.   
la configurazione è fatta in un file .yaml.   
componiamo dall'esempio sottostante il docker-compose.yaml:   
1. copio i vari nomi delle immagini come dizionario di nomi dei container   
2. copio le varie porte di comunicazione   
3. copio i vari link   
   
``` bash
redis:
	image: redis
db: 
	image: postgres:9.4
vote:
	image: voting-app
	#punto 2
	ports:
		- 5000:80
	#punto 3
	links:
		- redis-dns:redis
result:
	image: result-app
	#punto 2
	ports:
		- 5001:80
	#punto 3
	links:
		- postgres-dns:db
worker:
	image: worker
	#punto 3
	links:
		- redis-dns:redis
		- postgres-dns:db
```

### Docker links (deprecato)   
  
Prendiamo ad esempio un'applicazione composta da 5 container che compone il sistema di voto:   
1. voting-app: l'applicazione scritta in python che permette di visualizzare il frontend del processo di voto.   
2. in-memory DB: database redis dell'applicazione voting-app.   
3. worker: applicazione .net che gestisce il salvataggio tra in-memory DB e db persistente.   
4. db: database postgres SQL   
5. result-app: applicazione scritta in nodejs che espone il frontend dei dati scritti su db.   
   
potrebbero essere lanciate le varie applicazioni seguendo i comandi:   
```bash
#1
docker run -d --name=vote -p 5000:80 voting-app
#2
docker run -d --name=redis redis
#3
docker run -d --name=worker worker
#4
docker run -d --name=db postgres
#5
docker run -d --name=result -p 5001:80 result-app

```
il problema è che non avrò alcuna comunicazione tra i vari container lanciandoli in questo modo.   
il nome richiamato in docker run è il nome del dns della rete interna dei docker.   
proviamo a collegare i vari container   
```bash
#per prima cosa lancio i database:
docker run -d --name=redis redis
docker run -d --name=db postgres

#poi lancio il frontend
docker run -d --name=vote --link redis-dns:redis -p 5000:80 voting-app
docker run -d --name=result --link postgres-dns:db -p 5001:80 result-app

#quindi il backend
docker run -d  --link redis-dns:redis --link postgres-dns:db --name=worker worker
```

# Comandi   

## Run container   
```bash
docker run image-name<:tag>
#per attivare un docker con la modalità "interattiva" (accetta input dell'utente) si deve aggiungere -it
docker run -it image-name<:tag>

#Run - Port mapping
docker run -p <host-port>:<container-port> image-name<:tag>

#Run - Volume mapping
#docker container ha il proprio filesystem e non toccherà mai nulal fuori da esso
#per allocare dello spazio dell'host per il container allora utilizzare
docker run -v <host path>:<container path> image-name<:tag>
```
## List container   
```bash
# fa il list di tutti i container che sono in run
docker ps

# fa il list anche di tutti i container passati e fermi
docker ps -a
```
## Stop container   
```bash
docker stop <name>|<id>
```
## Remove container   
```bash
docker rm <name>|<id>
```
## List images   
```bash
docker images
```
## Remove images   
```bash
docker rmi <name>|<id>
```
## Pull image from Public Docker Registry   
```bash
docker pull <image name>
```
## Execute command on running container   
```bash
docker exec <container name>|<id> <command>
```
## Run endless container detaching it   
```bash
# avvia un docker mantenendosi attaccato al suo output. Può uscire premendo CTRL + C.
docker run <image name>

# aggiundere -d al comando s'ingifica che esso viaggerà per conto suo.
docker run -d <image name>

# per collegarsi al container basta indicare, possono essere anche solo i primi caratteri dell'id.
docker attach <id>
```
## Inspect container   
```bash
docker inspect <container name>|<id>
```
## Inspect Logs   
```bash
docker logs <container name>|<id>
```
   
