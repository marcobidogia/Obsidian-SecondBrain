---
tags:
  - programming_languages
  - go_lang
---
## Spiegazione Rapida
ecco una panorama veloce sui concetti base di Go (Golang) che ti aiuterà ad iniziare rapidamente a utilizzarlo in un ambiente di produzione:
#### 1. Package
Ogni programma Go inizia con un package. Il package main è speciale perché definisce un punto di ingresso eseguibile. Non un library package che viene usato come dipendenza.
```go
package main
```
#### 2. Import
Usa import per includere pacchetti esterni o standard library.
``` go
import "fmt"
```
#### 3. Funzione main
Il punto di ingresso di ogni programma Go è la funzione main nel package main.
```go
func main() {
    fmt.Println("Ciao, mondo!")
}
```
#### 4. Variabili
Le variabili possono essere dichiarate in modo esplicito o implicito con :=.
```go
var explicitVar int = 10
implicitVar := 20
```
#### 5. Tipi di Dati
Go ha tipi di dati built-in come int, float64, bool, e string. Supporta anche strutture dati complesse come array, slice, map, e struct.
#### 6. Controllo del Flusso
Go supporta istruzioni di controllo standard come if, else, switch, e cicli con for.
```go
for i := 0; i < 10; i++ {
    if i % 2 == 0 {
        fmt.Println(i, "è pari")
    } else {
        fmt.Println(i, "è dispari")
    }
}
```
#### 7. Funzioni
Le funzioni in Go possono avere parametri e più valori di ritorno.
``` go
func somma(a int, b int) (int, bool) {
    return a + b, true
}
```
#### 8. Concorrenza
Go rende la concorrenza gestibile e scalabile con goroutine e canali.
- Goroutine: una goroutine è una funzione che viene eseguita in modo concorrente.
```go
go myFunction()

```
- Canali: utilizzati per comunicare tra goroutine.
```go
ch := make(chan int)
```
#### 9. Struct e Interfacce
Le struct permettono di definire tipi personalizzati. Le interfacce definiscono insiemi di metodi.
```go
type Persona struct {
    Nome string
    Età  int
}

type Parlante interface {
    Parla() string
}
```
#### 10. Gestione degli Errori
Go affronta gli errori come valori ritornati. Non ci sono eccezioni.
```go
result, err := somma(1, 2)
if err != nil {
    fmt.Println("C'è stato un errore")
}
```
#### 11. Package e Gestione delle Dipendenze
Go utilizza go mod per la gestione delle dipendenze, facilitando l'aggiunta, la rimozione e l'aggiornamento dei pacchetti.
Questi concetti sono fondamentali per iniziare con Go. Man mano che ti immergi nello sviluppo con Go, esplorerai più dettagli e peculiarità del linguaggio che lo rendono un'ottima scelta per sistemi concorrenti, applicazioni web, servizi cloud, e molto altro.
### 12. Build
Per gestire il build delle applicazioni e' consigliato costruire un bash. Il comando per il build e':
``` bash
go build -o <nome_eseguibile> [<file_del_progetto>, ...]
```
## GoRoutine
In Go, la concorrenza è gestita tramite goroutine, che sono funzioni eseguite in modo concorrente. Le goroutine sono più leggere dei thread a livello di sistema e Go gestisce automaticamente la loro esecuzione su thread di sistema disponibili. Per eseguire due compiti in modo concorrente, puoi semplicemente avviare due goroutine. Qui sotto trovi un esempio di come fare:
#### Esempio di Due Goroutine
```go
package main

import (
    "fmt"
    "time"
)

// Definisci una funzione che verrà eseguita come goroutine
func faiQualcosa(messaggio string) {
    for i := 0; i < 5; i++ {
        fmt.Println(messaggio, ":", i)
        // Dormi un po' per simulare un lavoro che richiede tempo
        time.Sleep(time.Millisecond * 500)
    }
}

func main() {
    // Avvia la prima goroutine
    go faiQualcosa("goroutine 1")

    // Avvia la seconda goroutine
    go faiQualcosa("goroutine 2")

    // Aspetta un po' prima di terminare il programma principale
    // per permettere alle goroutine di completare il loro lavoro
    time.Sleep(time.Second * 5)
    fmt.Println("Finito")
}
```
### Cosa Succede in Questo Esempio:

1. **Definizione di Funzioni per Goroutine**: La funzione faiQualcosa stampa un messaggio più volte, dormendo un po' tra un messaggio e l'altro per simulare un compito che richiede tempo.
2. **Avvio delle Goroutine**: Usando la parola chiave go seguita da un invocazione di funzione ( go faiQualcosa("goroutine 1")), dici a Go di eseguire quella funzione in una nuova goroutine. Così facendo, faiQualcosa viene eseguita in modo concorrente al resto del programma.
3. **Attesa**: Poiché il main terminerebbe immediatamente dopo aver avviato le goroutine (terminando così anche tutte le goroutine prima che abbiano la possibilità di completare), time.Sleep viene usato nel main per aspettare abbastanza a lungo perché le goroutine completino il loro lavoro.

### Nota Importante:

L'uso di time.Sleep nel main è un modo semplice per aspettare le goroutine in questo esempio, ma non è una buona pratica per sincronizzare goroutine in programmi reali. Per sincronizzare goroutine e attendere che completino il loro lavoro, dovresti usare canali o altri meccanismi di sincronizzazione forniti da Go, come sync.WaitGroup.

Questo esempio dimostra il modo più basilare per eseguire compiti in modo concorrente in Go. Man mano che i tuoi programmi diventano più complessi, potresti dover gestire la comunicazione tra goroutine o sincronizzarle in modo più sofisticato.
## Test in Go
Sì, Go include un potente strumento integrato per il testing chiamato go test che ti permette di scrivere e eseguire test automatici per il tuo codice. I test in Go sono scritti come funzioni in file separati, tipicamente accanto al codice che testano, e possono essere facilmente eseguiti con il comando go test.
#### Come Scrivere un Test in Go
1. Crea un File di Test: I file di test sono solitamente posizionati nella stessa directory del codice che intendi testare. Il nome di un file di test segue il pattern nomefile_test.go.
2. Scrivi Funzioni di Test: Una funzione di test in Go inizia con la parola Test seguita da un nome (che deve iniziare con una lettera maiuscola). Accetta un singolo argomento di tipo \*testing.T.
Ecco un esempio di come potresti scrivere un semplice test:
Supponiamo di avere il seguente codice in calcolo.go:

```go
package calcolo

// Somma restituisce la somma di due interi.
func Somma(a, b int) int {
    return a + b
}
```
Puoi scrivere un test per questa funzione in calcolo_test.go:
```go
package calcolo

import "testing"

// TestSomma verifica la correttezza della funzione Somma.
func TestSomma(t *testing.T) {
    risultato := Somma(2, 3)
    atteso := 5
    if risultato != atteso {
        t.Errorf("Somma(2, 3) = %d; atteso %d", risultato, atteso)
    }
}
```
#### Come Eseguire i Test
Per eseguire i tuoi test, apri un terminale, naviga alla directory del tuo pacchetto e usa il comando go test. Se il test passa, go test si concluderà silenziosamente con un codice di stato 0. Se un test fallisce, go test stamperà i dettagli del fallimento e terminerà con un codice di stato non-zero.
```
shCopy code
go test

```
#### Testing Avanzato
Go supporta anche benchmarking e test di esempi. I benchmark sono scritti in modo simile ai test ma utilizzano \*testing.B e sono utili per misurare le prestazioni di parti del tuo codice. I test di esempi dimostrano come usare funzioni o pacchetti e possono essere eseguiti come test per verificare che il codice di esempio continui a funzionare come previsto.
Go offre anche meccanismi per testare il codice in modo più isolato attraverso mock e interfacce, permettendoti di scrivere test che non dipendono da dipendenze esterne come database o API web.
L'uso dei test in Go è un modo eccellente per assicurarsi che il tuo codice sia corretto, affidabile e facile da mantenere nel tempo.

## Context
In Go, context è un pacchetto che viene utilizzato per passare valori, segnali di cancellazione, e scadenze attraverso i confini delle API e tra goroutine. Il context.Context è un'interfaccia progettata per consentire a queste operazioni e più in generale per consentire di gestire la cancellazione e i timeout delle operazioni in modo coordinato.
La funzione context.Background() crea un nuovo contesto Context che non è mai cancellato, non ha valori e non ha scadenza. È inteso come il contesto di partenza da cui derivare altri contesti e tipicamente viene usato dall' main function, dall'inizializzazione globale, e nei test, come punto di partenza.
Ecco una spiegazione di var ctx = context.Background():
- var è una parola chiave utilizzata per dichiarare una variabile in Go.
- ctx è il nome della variabile, che è una convenzione comune per le variabili di tipo context.Context.
- context.Background() chiama la funzione Background del pacchetto context, che restituisce un contesto vuoto. Questo contesto è "vuoto" nel senso che non porta informazioni, non ha una deadline (scadenza) e non può essere cancellato.
Questo contesto base può essere utilizzato per derivare nuovi contesti con più informazioni specifiche, come timeout o segnali di cancellazione. Ecco alcuni esempi:
- Con Timeout: ctx, cancel := context.WithTimeout(context.Background(), 5\*time.Second) crea un nuovo contesto che verrà automaticamente cancellato dopo 5 secondi.
- Con Cancellazione: ctx, cancel := context.WithCancel(context.Background()) crea un nuovo contesto che può essere cancellato manualmente chiamando la funzione cancel().
Il pattern di utilizzo del contesto permette di gestire meglio le operazioni asincrone e le goroutine, offrendo un meccanismo per fermare le operazioni quando non sono più necessarie o quando sono richieste operazioni di pulizia.
## Terminazione sicura di un programma
Per gestire una terminazione sicura di un programma Go, specialmente di quelli che eseguono cicli infiniti o servizi che rimangono attivi per lungo tempo, puoi utilizzare i segnali del sistema operativo. Go fornisce il pacchetto os/signal per catturare e gestire i segnali inviati al tuo programma, consentendoti di eseguire una pulizia e uscire in modo controllato.
Ecco come puoi implementare una gestione della terminazione sicura in un'applicazione Go:
#### Passo 1: Importa i Pacchetti Necessari
```go
import (
    "context"
    "fmt"
    "os"
    "os/signal"
    "syscall"
    "time"
)
```
#### Passo 2: Prepara un Canale per i Segnali
Devi creare un canale Go per ricevere segnali di sistema. Poi, utilizzerai signal.Notify per dire al pacchetto os/signal di inviare segnali di interesse, come SIGINT (Ctrl+C) o SIGTERM (comando di terminazione), a quel canale.
```go
signals := make(chan os.Signal, 1)
signal.Notify(signals, syscall.SIGINT, syscall.SIGTERM)
```
#### Passo 3: Usa un Context con Cancellazione
Per gestire la cancellazione in modo più ordinato, soprattutto se hai molteplici goroutine o operazioni pendenti, puoi utilizzare context.WithCancel.
```go
ctx, cancel := context.WithCancel(context.Background())
```
#### Passo 4: Avvia il Ciclo Infinito e Ascolta i Segnali
Qui combineremo un ciclo infinito con l'ascolto dei segnali. Quando riceviamo un segnale, invocheremo la funzione cancel per segnalare a tutte le parti del programma che è il momento di pulire e uscire.
```go
go func() {
    for {
        select {
        case <-ctx.Done():
            fmt.Println("Pulizia e uscita...")
            // Qui inserisci la logica di pulizia
            os.Exit(0)
        default:
            // La tua logica di ciclo infinito va qui
            fmt.Println("Esecuzione...")
            time.Sleep(2 * time.Second)
        }
    }
}()

// Aspetta un segnale di terminazione
<-signals
cancel() // Segnala la cancellazione al contesto, che ferma il ciclo infinito
```
#### Esempio Completo
Combinando tutto insieme, ecco come potrebbe apparire il tuo programma:
```go
package main

import (
    "context"
    "fmt"
    "os"
    "os/signal"
    "syscall"
    "time"
)

func main() {
    ctx, cancel := context.WithCancel(context.Background())

    signals := make(chan os.Signal, 1)
    signal.Notify(signals, syscall.SIGINT, syscall.SIGTERM)

    go func() {
        for {
            select {
            case <-ctx.Done():
                fmt.Println("Pulizia e uscita...")
                // Inserisci qui la logica di pulizia
                return
            default:
                fmt.Println("Esecuzione...")
                time.Sleep(2 * time.Second)
            }
        }
    }()

    // Aspetta un segnale
    <-signals
    cancel() // Invia il segnale di cancellazione

    // Attendi che tutte le pulizie siano complete
    // Potresti voler usare un WaitGroup o un altro meccanismo di sincronizzazione
    // per assicurarti che tutte le goroutine abbiano finito prima di uscire definitivamente.
    time.Sleep(1 * time.Second) // Esempio di attesa; adatta secondo necessità
    fmt.Println("Programma terminato.")
}
```
Questo approccio ti permette di interrompere il tuo ciclo infinito o servizio in modo sicuro, dando al tuo programma la possibilità di eseguire operazioni di pulizia necessarie prima di terminare.

- se facessi un process kill per fermare il processo come posso gestire la chiusura sicura?

Se il tuo programma Go viene terminato tramite un comando kill (es. kill \<pid> su sistemi Unix-like), puoi gestire una chiusura sicura ascoltando per i segnali SIGINT (interruzione da tastiera, Ctrl+C) e SIGTERM (il segnale di terminazione di default inviato da kill). Per i segnali inviati direttamente al processo, come SIGKILL (es. kill -9 \<pid>), non c'è modo di intercettarli o gestirli in quanto il sistema operativo termina il processo immediatamente senza invocare la gestione dei segnali nel processo.
Ecco come puoi ascoltare i segnali SIGINT e SIGTERM per chiudere in modo pulito il tuo programma Go:

```go
package main

import (
    "context"
    "fmt"
    "os"
    "os/signal"
    "syscall"
    "time"
)

func main() {
    // Prepara un context che possa essere cancellato
    ctx, cancel := context.WithCancel(context.Background())

    // Crea un canale per ascoltare i segnali del sistema operativo
    signals := make(chan os.Signal, 1)
    // Notifica il canale in caso di SIGINT o SIGTERM
    signal.Notify(signals, syscall.SIGINT, syscall.SIGTERM)

    // Goroutine che simula un lavoro a lungo termine
    go func() {
        for {
            select {
            case <-ctx.Done(): // Controlla se il contesto è stato cancellato
                fmt.Println("Esecuzione delle operazioni di pulizia...")
                // Inserisci qui la tua logica di pulizia
                fmt.Println("Operazioni di pulizia completate, uscita.")
                return
            default:
                // La tua logica di business regolare va qui
                fmt.Println("Esecuzione...")
                time.Sleep(2 * time.Second) // Simula un lavoro
            }
        }
    }()

    // Aspetta di ricevere un segnale
    <-signals
    fmt.Println("Segnale ricevuto, iniziando la procedura di chiusura...")
    cancel() // Cancella il context per far sapere alle goroutine di terminare

    // Assicurati che tutte le goroutine abbiano tempo di chiudersi pulitamente
    time.Sleep(1 * time.Second) // Questo è solo un esempio, adatta in base alle tue esigenze

    // Puoi implementare qui ulteriori logiche di attesa se necessario,
    // ad esempio aspettando un gruppo di attesa (sync.WaitGroup) se vuoi
    // assicurarti che tutte le tue goroutine siano terminate prima di uscire.

    fmt.Println("Programma terminato.")
}
```
Questo codice si prepara a gestire una chiusura pulita in caso di segnali di terminazione, come quelli inviati dal comando kill senza l'uso dell'opzione -9. Si basa su un contesto cancellabile per notificare a tutte le parti interessate del programma che è il momento di terminare. Quando il segnale viene ricevuto, il programma esegue le operazioni di pulizia necessarie prima di uscire definitivamente.
Ricorda: non c'è modo di gestire o intercettare il segnale SIGKILL ( kill -9), poiché questo segnale è gestito direttamente dal kernel e termina il processo immediatamente. Per questo motivo, quando possibile, è preferibile utilizzare segnali che possono essere intercettati e gestiti, come SIGINT o SIGTERM, per terminare un processo, permettendo al tuo programma di chiudere le risorse in modo pulito.
## Array
### Join
In Go, non esiste una funzione built-in specifica per fare il "join" di due array o slice direttamente, come potresti trovare in altri linguaggi di programmazione. Tuttavia, puoi facilmente combinare due slice utilizzando un ciclo o, in modo più idiomatico, sfruttando la funzione append. Ecco come puoi fare:
#### Unire Due Slice con append
Se hai due slice di tipo omogeneo (ovvero, dello stesso tipo) e vuoi unirli in un'unica slice, puoi usare append in questo modo:
```go
package main

import "fmt"

func main() {
    slice1 := []int{1, 2, 3}
    slice2 := []int{4, 5, 6}

    // Unisce slice1 e slice2
    sliceUnite := append(slice1, slice2...)

    fmt.Println(sliceUnite) // Output: [1 2 3 4 5 6]
}
```
In questo esempio, slice1 e slice2 sono due slice di interi. Utilizziamo append per aggiungere tutti gli elementi di slice2 alla fine di slice1. L'operatore ... dopo slice2 è essenziale perché scompone la slice in elementi individuali, permettendo a append di accettarli come argomenti variadici.
#### Nota sui Tipi
Il metodo sopra funziona solo se le due slice sono dello stesso tipo. Se hai bisogno di unire slice di tipi diversi, dovresti considerare se questo è realmente necessario, poiché in Go è generalmente preferibile lavorare con tipi omogenei. Un'opzione potrebbe essere definire una slice di un tipo interfaccia se i tipi coinvolti hanno un insieme comune di metodi, oppure utilizzare una slice di interface{} se non esiste una tale interfaccia comune, ma questa soluzione dovrebbe essere usata con cautela per evitare di perdere i vantaggi del tipaggio statico.
#### Performance
L'uso di append in questo modo è generalmente efficiente, ma se sai già la lunghezza totale della slice risultante, può essere leggermente più performante pre-alloccare la slice della dimensione appropriata e copiare gli elementi direttamente. Questo può ridurre il numero di allocazioni di memoria necessarie quando la slice risultante cresce.
Ecco come potresti fare se vuoi pre-alloccare la slice:
```go
sliceUnite := make([]int, 0, len(slice1)+len(slice2))
sliceUnite = append(sliceUnite, slice1...)
sliceUnite = append(sliceUnite, slice2...)
```

Questo approccio pre-alloca una slice ( sliceUnite) della dimensione esatta necessaria per contenere tutti gli elementi di slice1 e slice2, e poi usa append per popolare sliceUnite con gli elementi di entrambe le slice.