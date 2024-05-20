---
tags:
  - course
  - programming_languages
  - refactoring
---
## Code smells
I code smell sono i sintomi di un refactoring necessario. Esistono diversi tipi di code smell e sono tutti dei modi di scrivere il codice che ne minano l'affidabilità etc.

Bloaters
Sono il codice, il metodo e le classi che si ingrandiscono e rendono difficile lavorarli. Normalmente sono "smells" che si accumulano nel tempo.

### Long Methods
I metodi che contengono molte linee di codice, generalmente i metodi che sono più lunghi di 10 righe dovrebbero mettere in guardia il programmatore.
E' comune la mentalità di programmatori i quali devono aggiungere "solo due linee di codice" e non creano un metodo ma lo mettono in coda ad uno esistente, questo è un modo per dare inizio ad un "spaghetti code".

Trattamento:
Il trattamento principale è quello di prendere l'intera funzione e spezzarla in metodi piccoli e con nomi parlanti, in modo che nessuno ne debba leggere il codice per capire cosa facciano.

#### 1. Extract Method
Problem
You have a code fragment that can be grouped together.
```c#
void PrintOwing()
{
  this.PrintBanner();

  // Print details.
  Console.WriteLine("name: " + this.name);
  Console.WriteLine("amount: " + this.GetOutstanding());
}
```
Solution
Move this code to a separate new method (or function) and replace the old code with a call to the method.
```c#
void PrintOwing()
{
  this.PrintBanner();
  this.PrintDetails();
}

void PrintDetails()
{
  Console.WriteLine("name: " + this.name);
  Console.WriteLine("amount: " + this.GetOutstanding());
}
```

#### 1.1. Reduce Local Variables and Parameters Before Extracting a Method
If local variables and parameters interfere with extracting a method, use Replace Temp with Query, Introduce Parameter Object or Preserve Whole Object.

Problem
You place the result of an expression in a local variable for later use in your code.
```c#
double CalculateTotal()
{
  double basePrice = quantity * itemPrice;

  if (basePrice > 1000)
  {
    return basePrice * 0.95;
  }
  else
  {
    return basePrice * 0.98;
  }
}
```

Solution
Move the entire expression to a separate method and return the result from it. Query the method instead of using a variable. Incorporate the new method in other methods, if necessary.
```c# 
double CalculateTotal()
{
  if (BasePrice() > 1000)
  {
    return BasePrice() * 0.95;
  }
  else
  {
    return BasePrice() * 0.98;
  }
}
double BasePrice()
{
  return quantity * itemPrice;
}
```
#### 1.2. Parameter Object
Problem
Your methods contain a repeating group of parameters.
Transform the method into a separate class so that the local variables become fields of the class. Then you can split the method into several methods within the same class.
```c#
public class Order
{
  // ...
  public double Price()
  {
    return new PriceCalculator(this).Compute();
  }
}

public class PriceCalculator
{
  private double primaryBasePrice;
  private double secondaryBasePrice;
  private double tertiaryBasePrice;

  public PriceCalculator(Order order)
  {
    // Copy relevant information from the
    // order object.
  }

  public double Compute()
  {
    // Perform long computation.
  }
}
```
#### 1.2. Parameter Object
Problem
Your methods contain a repeating group of parameters.
Solution
Replace these parameters with an object.

#### 1.3. Preserve Whole Object
Problem
You get several values from an object and then pass them as parameters to a method.

```c#
int low = daysTempRange.GetLow();
int high = daysTempRange.GetHigh();
bool withinPlan = plan.WithinRange(low, high);```

Solution
Instead, try passing the whole object.
```c#
bool withinPlan = plan.WithinRange(daysTempRange);
```

#### 1.4. Replace Method with Method Object
Problem
You have a long method in which the local variables are so intertwined that you can't apply Extract Method.
```c#
public class Order
{
  // ...
  public double Price()
  {
    double primaryBasePrice;
    double secondaryBasePrice;
    double tertiaryBasePrice;
    // Perform long computation.
  }
}
```
Solution
Transform the method into a separate class so that the local variables become fields of the class. Then you can split the method into several methods within the same class.
```c#
public class Order
{
  // ...
  public double Price()
  {
    return new PriceCalculator(this).Compute();
  }
}

public class PriceCalculator
{
  private double primaryBasePrice;
  private double secondaryBasePrice;
  private double tertiaryBasePrice;

  public PriceCalculator(Order order)
  {
    // Copy relevant information from the
    // order object.
  }

  public double Compute()
  {
    // Perform long computation.
  }
}
```

#### 2. Conditionals and Loops
Operatori condizionali e loop sono buoni collanti di codice e possono essere spostati per separare i metodi

#### 2.1 Decompose Conditional
Problem
You have a complex conditional ( if-then/ else or switch).
```c#
if (date < SUMMER_START || date > SUMMER_END)
{
  charge = quantity * winterRate + winterServiceCharge;
}
else
{
  charge = quantity * summerRate;
}
```
Solution
Decompose the complicated parts of the conditional into separate methods: the condition, then and else.
```c#
if (isSummer(date))
{
  charge = SummerCharge(quantity);
}
else
{
  charge = WinterCharge(quantity);
}```

#### 2.2. Extract Method
Problem
You have a code fragment that can be grouped together.
```c#
void printProperties(IList users)
{
  for (int i = 0; i < users.size(); i++)
  {
    string result = "";
    result += users.get(i).getName();
    result += " ";
    result += users.get(i).getAge();
    Console.WriteLine(result);

    // ...
  }
}
```
Solution
Move this code to a separate new method (or function) and replace the old code with a call to the method.
```c#
void printProperties(IList users)
{
  foreach (User user in users)
  {
    Console.WriteLine(getProperties(user));

    // ...
  }
}

string getProperties(User user)
{
  return user.getName() + " " + user.getAge();
}
```
#### 3. Extract Interface
Problem
Multiple clients are using the same part of a class interface. Another case: part of the interface in two classes is the same.

### Large Class
Classi che contengono molte proprietà, metodi e linee di codice

#### 1. Extract Class
Problem
When one class does the work of two, awkwardness results.
Solution
Instead, create a new class and place the fields and methods responsible for the relevant functionality in it.

#### 2. Extract Subclass
Problem
A class has features that are used only in certain cases.
Solution
Create a subclass and use it in these cases.
Solution
Move this identical portion to its own interface.

#### 4. Separate GUI and Domain Data
Problem
Is domain data stored in classes responsible for the GUI?
Solution
Then it's a good idea to separate the data into separate classes, ensuring connection and synchronization between the domain class and the GUI.

#### 4. Get Rid of Type Codes
Problem
A class has a field that contains type code. The values of this type aren't used in operator conditions and don't affect the behavior of the program.
### Primitive Obsession
Usare tipi primitivi rispetto a piccoli oggetti per piccoli e semplici task.
Come la maggior parte degli altri smell, la primitive obsession nasce nei momenti di debolezza. "Solo un campo per memorizzare alcuni dati!" disse il programmatore. Creare un campo primitivo è molto più semplice che creare una classe completamente nuova, giusto? E così è stato fatto. Quindi è stato necessario un altro campo ed è stato aggiunto allo stesso modo. Ecco, la classe divenne enorme e ingombrante.

#### 1. Replace Set of Fields with Object
Problem
A class (or group of classes) contains a data field. The field has its own behavior and associated data.
Solution
Create a new class, place the old field and its behavior in the class, and store the object of the class in the original class.

#### 2. Primitive Fields in Method Parameters
Problem
Your methods contain a repeating group of parameters.
Solution
Replace these parameters with an object.
#### 3. Preserve Whole Object
Problem
You get several values from an object and then pass them as parameters to a method.
```c#
int low = daysTempRange.GetLow();
int high = daysTempRange.GetHigh();
bool withinPlan = plan.WithinRange(low, high);
```

Solution
Instead, try passing the whole object.
```c#
bool withinPlan = plan.WithinRange(daysTempRange);
```
Solution
Create a new class and use its objects instead of the type code values.

#### 5. Replace Type Code with Subclasses
Problem
You have a coded type that directly affects program behavior (values of this field trigger various code in conditionals).
Solution
Create subclasses for each value of the coded type. Then extract the relevant behaviors from the original class to these subclasses. Replace the control flow code with polymorphism.

#### 6. Replace Type Code with State/Strategy
When complicated data is coded in variables, use Replace Type Code with Class, Replace Type Code with Subclasses or Replace Type Code with State/Strategy.
Problem
You have a coded type that affects behavior but you can't use subclasses to get rid of it.
Solution
Replace type code with a state object. If it's necessary to replace a field value with type code, another state object is "plugged in".

#### 7. Replace Array with Object
Problem
You have an array that contains various types of data.
```c#
string[] row = new string[2];
row[0] = "Liverpool";
row[1] = "15";
```
Solution
Replace the array with an object that will have separate fields for each element.
```c#
Performance row = new Performance();
row.SetName("Liverpool");
row.SetWins("15");
```

### Long Parameter List
Potrebbe verificarsi un lungo elenco di parametri dopo che diversi tipi di algoritmi vengono uniti in un unico metodo. Potrebbe essere stato creato un lungo elenco per controllare quale algoritmo verrà eseguito e come.
Lunghi elenchi di parametri possono anche essere il risultato degli sforzi volti a rendere le classi più indipendenti le une dalle altre. Ad esempio, il codice per creare oggetti specifici necessari in un metodo è stato spostato dal metodo al codice per chiamare il metodo, ma gli oggetti creati vengono passati al metodo come parametri. Pertanto la classe originale non conosce più le relazioni tra gli oggetti e la dipendenza è diminuita. Ma se vengono creati più di questi oggetti, ognuno di essi richiederà il proprio parametro, il che significa un elenco di parametri più lungo.
È difficile comprendere tali elenchi, che diventano contraddittori e difficili da usare man mano che si allungano. Invece di un lungo elenco di parametri, un metodo può utilizzare i dati del proprio oggetto. Se l'oggetto corrente non contiene tutti i dati necessari, è possibile passare un altro oggetto (che otterrà i dati necessari) come parametro del metodo.

#### 1. Replace Parameter with Method Call
Problem
Calling a query method and passing its results as the parameters of another method, while that method could call the query directly.
```c#
int basePrice = quantity * itemPrice;
double seasonDiscount = this.GetSeasonalDiscount();
double fees = this.GetFees();
double finalPrice = DiscountedPrice(basePrice, seasonDiscount, fees);
```
Solution
Instead of passing the value through a parameter, try placing a query call inside the method body.
```c#
int basePrice = quantity * itemPrice;
double finalPrice = DiscountedPrice(basePrice);
```
