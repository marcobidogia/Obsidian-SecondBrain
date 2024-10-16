---
tags:
  - design_patterns
  - dependency-injection
link: https://learn.microsoft.com/en-us/dotnet/core/extensions/dependency-injection https://medium.com/@anyanwuraphaelc/dependency-injection-design-patterns-in-c-b982c141dcb2
---
[Dependency injection fundamentals in C# - DI vs IoC vs DIP](https://www.youtube.com/watch?v=M1jxLQu40qo)
# Cos'é il dipendency inversion principle
É un modo di progettare il software in modo che esistano delle interfacce le quali rendono semplice l'integrazione con degli oggetti simili tra di loro. Oltre a questo aspetto si intende dipendency inversion principle anche quel processo di passaggio di responsabilitá alle classe che avranno effettivamente il compito di gestire quella funzione. Ultima ma non per importanza, nel caso di dipendency inversion principle si puó anche pensare che le singole librerie, che per comunicare tra di loro nel modo normale necessitano di dipendenze definite, possano dialogare anche con delle librerie che non si conoscono, quindi si evitano diversi problemi di importazioni di classi esose dal punto di vista del peso.

![[./media/Pasted image 20240823145433.png|Pasted image 20240823145433.png]]

Nell'immagine di sopra ecco un esempio di classe standard e classe gestita dall principio di dipendency inversion principle.

Serve a spiegare come "rompere" il progetto in classi non collegate sia meglio, tendenzialmente tra un punto ed un altro si parla attraverso delle interfacce.

# Cos'é la dependency inversion control principle
É il principio di design per il quale viene dato una parte del controllo del tuo sistema, oggetti o porzioni del tuo programma, a qualche container o framework.

Nella programmazione normale dove il programma fruisce da sopra a sotto, sono responsabile di generare classi e gestirne le istanze. Nel principo dell'inversione del controllo passo una parte di questa responsabilitá ad un container o ad un framework.
Dependency injection é il metodo di implementare il principio di inversione del controllo.

# Esistono 3 tipi di dependency injection
## Constructor injection
Nel costruttore dell'oggetto passi l'istanza che implementa la tua interfaccia direttamente all'oggetto che la necessita.
## Setter injection
Nell'oggetto ci sará un costruttore che ne setterá l'istanza che implementa l'interfaccia di controllo.
## Interfacer injector
Nell'oggetto c'é un interfaccia che implementa un setter che imposterá l'istanza che implementa l'interfaccia di controllo.

L'estensione [Microsoft.Extensions.DependencyInjection](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.dependencyinjection.iservicescopefactory) di C# implementa il Service Collection:
# [Microsoft.Extensions.DependencyInjection](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.dependencyinjection.iservicescopefactory)
É l'il framework che gestisce in modo autonomo da .Net la creazione di istanze che utilizzano il principio di dependency inversion:

quello che nel codice scriverei:

```C#
Console.WriteLine(new StudentListService(new StudentList()).GetBetterStudent())

class StudentListService(IStudentList studentList)
{
	IStudentList _studentList = studentList
	public string GetBetterStudent()
	{
		return studentList.GetBetterStudent()
	}
	
	// do stuff
}

interface IStudentList
{
	string GetBetterStudent();
}

class StudentList: IStudentList
{
	public string GetBetterStudent() => return betterStudent
}
```

Con la libreria diventerebbe:

```C#
using Microsoft.Extensions.DependencyInjection;

var serviceCollection = new ServiceCollection()

serviceCollection.AddTransient<IStudentList, StudentList>();
serviceCollection.AddTransient<StudentListService>();

StudentListService sls = serviceCollection.GetRequiredService<StudentListService>();
Console.WriteLine(sls.GetBetterStudent());

class StudentListService(IStudentList studentList)
{
	IStudentList _studentList = studentList
	public string GetBetterStudent()
	{
		return studentList.GetBetterStudent()
	}
	
	// do stuff
}

interface IStudentList
{
	string GetBetterStudent();
}

class StudentList: IStudentList
{
	public string GetBetterStudent() => return betterStudent
}

```

Cosa succede, il framework definisce gli oggetti che gli servono per eseguire la funzione di `GetBetterStudent` ma in modo gestito dal framework .Net quindi meglio ottimizzato.

Il codice fa questo:
1. eseguendo `StudentListService sls = serviceCollection.GetRequiredService<StudentListService>();` richiede un'istanza di StudentListService
2. StudentListService dipende da IStudentList, che viene risolta, come da riga `serviceCollection.AddTransient<IStudentList, StudentList>();` in StudentList
3. per generare StudentService crea un'istanza di StudentList che implementa IStudentList e un'istanza StudentListService.

## AddTransient
Indica che l'istanza viene generata come nuova ogni volta che qualcuno la richiede.

## AddScoped
Indica che l'istanza viene generata per un'unitá di tempo decisa dal client.

## AddSingleton
Indica che l'istanza viene generata una volta per sempre.