---
tags:
  - aws
---
### Generale
IAM è il servizio di gestione degli account di AWS a livello globale.
Al momento della creazione del primo account verrà generato un account root il quale ha accesso da amministratore.

> [!info] Best Practise
> L'utente root non deve essere utilizzato o condiviso con gli altri utenti nel normale funzionamento

#### Users
Gli utenti "users" sono le persone fisiche comprese nella tua organizzazione e possono essere raggruppate
#### Groups
I gruppi contengono solo utenti e non altri gruppi. Sono un'insieme di utenti e vengono usati per dividere le divisioni che accedono al cloud
### Permissions
Per ogni utente è possibile gestire l'accesso ad ogni singola api di AWS.

>[!info] Best Practise
 Per ogni utente sarà buona norma dare solo i permessi richiesti per eseguire i suoi compiti e nulla di più. Questo principio viene chiamato least privilege principle
 La policy ([[IAM#Policy]]) è un documento JSON che espone i permessi dell'utente.

#### Policy
Esprime grazie un documento JSON i permessi che possono essere riferiti ad uno o più utenti
Es.
```json
{ 
 "Version": "2012-10-17", 
 "Statement": 
 [ 
  { 
   "Effect": "Allow",
   "Action": "ec2:Describe*", 
   "Resource": "*"
  }, 
  { 
   "Effect": "Allow", 
   "Action": "elasticloadbalancing:Describe*", 
   "Resource": "*" 
  }, 
  { 
   "Effect": "Allow", 
   "Action": [ "cloudwatch:ListMetrics", "cloudwatch:GetMetricStatistics", "cloudwatch:Describe*" ], 
   "Resource": "*" 
  } 
 ] 
}
```

#### Struttura di una policy
Consiste in:
- "Version": la versione della policy, normalmente "2012-10-17"
- "Id" (optional): è l'identificatore della policy
- "Statements": normalmente una o più dichiarazione o regola e consiste in:
- "Sid" (optional): l'identificatore della dichiarazione.
- "Effect": indica se l'effetto della dichiarazione è di permissione o negazione della regola, infatti può avere i valori:
- "Allow" per consentire
- "Deny" per negare
- "Principal": indica l'utente ([[IAM#Users]]), l'account o il ruolo ([[IAM#Role]]) a cui la policy e riferita.
- "Action": indica la lista di azioni da permettere o negare, ad esempio:
```json
{
 "Effect":"Allow",
 "Action":[
 "s3:GetObject",
 "s3:PutObject"
 ]
}
```
in questo caso vengono permesse le funzioni di raccolta e di aggiunta di un oggetto da s3.
- "Resource": indica la risorsa a cui queste azioni sono applicate es: "arn:aws:s3:::mybucket/\*" indica che l'azione sarà permessa solo per il bucket con l'arn inserito.
- "Condition" (optional): possono essere inserite anche delle condizioni per le quali la policy entra in funzione
#### Password Policy
In AWS la sicurezza sta al primo posto e quindi anche gestire delle password complesse deve essere una priorità.
E' possibile settare una policy che obbliga i propri utenti ad avere una password con i seguenti requisiti:
- Minima lunghezza della password.
- Richiedere specifici caratteri:
- Lettere in uppercase
- Lettere in lowercase