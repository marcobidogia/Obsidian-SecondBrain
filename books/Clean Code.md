---
tags:
  - books
  - programming_languages
  - coding
---
### Blocchi Funzione
Dal libro si evince che Robert all'inizio della propria carriera abbia lavorato creando programmi che creavano delle routines subroutines le quali erano male organizzate e troppo prolisse. Nel caso specifico a pagina 32 mostra del codice che poteva essere facilmente ripreso e ritrattato per renderlo più leggibile e più chiaro a tutti. Nello specifico ha creato delle funzioni che portavano via molto codice che veniva scritto più volte all'interno del metodo.
#robert_c_martin descrive i seguenti 2 aspetti:
#### 1. Small!
La prima regola è che una funzione dovrebbe essere piccola. La seconda regola è che una funzione deve essere ancora più piccola di quanto lo sia in realtà. Vuol dire che una funzione normalmente viene scritta un po' a sentimento ma con l'andare del tempo viene facilitata sempre di più per renderla più agile e più semplice da manutenzionare.
#### 2. Do One Thing
Dopo 30 anni di lavoro Robert espime un pensiero:
> [!QUOTE]
FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT WELL. THEY SHOULD DO IT ONLY
Per fare in modo che questa cosa accada è necessario pensare a cosa debba fare questa funzione: ad esempio.

> [!QUOTE]
TO render page with setups and teardowns, we check to see whether the page is a test page and if so, we include the setups and teardowns. In either case we render the page in HTML
Se all'interno della frase esiste solo un TO allora è la funzione farà solo 1; cosa nel caso contrario ne farà più di una e quindi dovrà essere divisa.
### Meaningful Names
Scegliere nomi Intenction-Revealing per le variabili è importante in quanto riusciranno a rendere più leggibile il tuo codice. In questo esempio la variabile var-1 è stata definita con il nome di "d", poi le viene data una descrizione di quello che fa nel commento a suo seguito. Perchè non dare direttamente un nome parlante alla variabile quindi al posto di "d" -> "elapsedTimeInDays". Questo stratagemma rende molto più leggibile il codice e fa capire cosa le variabili sono atte a fare.

```c#
//var-1
int d; //elapsed time in days

//var-1*
int elapsedTimeInDays;
```
---
Propongo questo codice:
```c#
public List<int[]> getThem()
{
 List<int[]> list1 = new List<int[]>();
 foreach(int[] x in TheList)
 {
  if(x[0] == 4)
   list1.Add(x);
 }
 return list1
}
```

Un codice del genere è poco parlante, è molto difficile capire dove possa andare a parare. Nel caso specifico di questa funzione essa è atta a selezionare da una game board tutte le celle flaggate. Semplicemente cambiano il nome delle variabili, definendo una classe "Cell" e una funzione "IsFlagged()", che risponde true se il valore di Cell[0] sia uguale a 4, il tutto risulta molto più chiaro e leggibile:

```c#
public List<Cell> GetFlaggedCells()
{
 List<Cell> fleggedCells = new List<Cell>();
 foreach(Cell cell in gameBoard)
 {
  if(cell.isFlegged())
   fleggedCells.Add(x);
 }
 return fleggedCells
}
```

Il succo del discorso sta nell'usare quanto più possibile dei nomi semplici, facilmente pronunciabili e facilmente ricercabili, ad esempio non vale la pena dare un nome "genymdhms" (generation year month day hour seconds) ma meglio "generationTimespan".
E' molto utile definire un proprio standard di nomenclatura, ad esempio le variabili globali e costanti indicarle tutte in maiuscolo, quelle più secondarie utilizzare un nome in minuscolo. Potrebbero essere usate variabili composte da singole lettere SOLO all'interno di rapide funzioni.