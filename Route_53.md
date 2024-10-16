---
tags:
  - aws
---
## Intro
### DNS
Un DNS (Domain Name System) è un sistema che traduce un hostname human friendly in un indirizzo IP di una macchina. Ad esempio scrivendo su un browser "www.google.com" esso verrà tradotto con l'indirizzo IP della macchina in cui risiede il web server. Quindi si può dire che il DNS è la spina dorsale di internet, usa una gerarchia:
1. .com
2. example.com
3. www.example.com
4. api.example.com

#### Terminologia
- Domain Registrar: è la società che si occupa di registrare i domini, ad esempio: Amazon Route53, GoDaddy o qualsiasi altro registratore di domini.
- DNS records: ne esistono di diversi tipi e saranno visti poi nello specifico, A, AAAA, CNAME, NS... ().
- Zone file: è in punto che contiene ogni corrispondenza IP Address --> DNS Name.
- Name Server: Sono i server che risolvono i DNS.
- Root: il punto alla fine nel DNS.
- Top Level Domains (TLD): sono i domini di primo livello ovvero, .com, .net, .it...
- Second Level Domains (SLD): sono i domini con 2 parole, amazon.com, google.it...
- Sub domain: ovvero tutto ciò che si trova dopo www.*
- Fully Qualified Domain Name (FQDN): il nome completo con tutto ciò che c'è dopo il protocollo fino alla fine del DNS.
- Protocol: il protocollo di scambio verso il DNS.

#### Come lavorando i DNS
Ecco un semplice esempio di come funziona la risoluzione di un DNS.
Abbiamo creato un web server su una macchina con indirizzo IP pubblico "9.10.11.12" e quindi abbiamo registrato sul nostro Domain Registrar (ROUTE 53) il nome DNS "example.com".
Dal Web Browser vogliamo cercare il web server esposto dalla macchina grazie al DNS.
Cerchiamo quindi sul nostro Browser "example.com", la richiesta verrà inviata al nostro DNS Server locale che, consideriamo sia la prima volta che questo dominio venga richiesto, non conosce il dominio. Quindi il Local DNS Server andrà a chiedere al Root DNS Server (un server di Root gestito dalla compagnia ICANN): "Dammi l'indirizzo IP del mio DNS "example.com"". Il Root DNS Server risponderà per la sua parte di pertinenza del DNS che è ".com": "per me il root .com ha come IP 1.2.3.4". A seguito di questa risposta il Local DNS Server chiederà al TLD DNS Server di fornirgli l'IP del DNS "example.com", questo risponderà: "Non so quale sia il record ma c'è un server che conosco che si chiama "example.com", il suo IP pubblico è 5.6.7.8". Quindi, Il Local DNS Server chiederà al Domain Registrar se conosce l'indirizzo IP legato al DNS "example.com". Il SLD DNS Server conosce bene l'indirizzo IP del DNS "example.com" e ne restituisce il valore al Local DNS Server. Il Local DNS Server salverà in cache l'indirizzo IP e lo terrà valido per un tempo chiamato "TTL". L'indirizzo IP passerà quindi al Web Browser, che salverà a sua volta su una cache per il tempo "TTL", e quindi passerà a lanciare la ricerca per collegarsi al Web Server.

i## Cos'è Route53
Route53 è un highly available, scalable, fully managed, authoritative (il cliente (tu) può modificare autonomamente i DNS) DNS Domain Registrar.