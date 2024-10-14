---
tags:
  - coding
  - dotnet
  - clean-architecture
---
# Intro
Dependency injection è un pattern di sviluppo di dotnet utile per spezzare il programma in molti piccoli servizi. I servizi sono gestiti interamente dal framework.

# Configurare un servizio
È possibile configurare un servizio in 2 modi:

## 1. Classe di appoggio

Per configurare il servizio grazie ad una classe d'appoggio sarà necessario creare una classe (magari con un record o una classe specifica) in cui saranno appoggiate le impostazioni da dare.

Grazie all'HostApplicationBuilder sarà possibile recuperare le informazioni dal file appsettings.json sulla cartella di sviluppo. Per passare le impostazioni sará necessario chiamare la seguente linea di codice:
```c#
 builder.Services.Configure<TClassOption>(builder.Configuration.GetSection("<section>"));
```

Per recuperare tali informazioni sul costruttore di classe del servizio sará necessario impostar il parametro: 
```c#
 IOptions<TClassOption> option
```
Con questo sará possibile recuperare le informazioni del file appsettings.json.

## 2. Interfaccia generica

Sul costruttore del servizio sará possibile passare il parametro: 
```c#
IConfiguration configuration
```

dove sarà possibile reperire le impostazioni cercando con il seguente pattern:
```c#
 configuration["<Section>:<SubSection|Parameter>]
```