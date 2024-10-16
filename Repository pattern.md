---
tags:
  - dotnet
  - clean-architecture
  - design_patterns
---
https://medium.com/@pererikbergman/repository-design-pattern-e28c0f3e4a30
https://www.youtube.com/watch?v=h4KIngWVpfU&t=3s

# Cos'è
Il repository patter è un modo di affrontare il problema del recupero di dati dal database in modo strutturato, principalmente con metodi come [[./Entity framework|Entity framework]].

Per rendere pratico e dinamico l'approccio a questo metodo divido le forme dei dati per astrazioni:

## Models
I modelli sono la forma più vicina al database. Configurano la disposizione della tabella o del documento dove risiedono i dati.

## Records
I record sono la forma "evoluta" dei [[Repository pattern#Models|Repository pattern > Models]]. Tendenzialmente sono l'oggetto che viene utilizzato nell'applicazione. Possono essere una parte o interamente parte di un modello o anche una composizione di più modelli stessi.

## Repository
Le repository sono il punto di incontro tra [[Repository pattern#Models|Repository pattern > Models]] e [[Repository pattern#Records|Repository pattern > Records]].
Una repository corrisponde ad un insieme di metodi e funzionalità astratte che compongono dai models i records.

## Esempio
Su database esiste una tabella chiamata studenti e una chiamata voti che si riferiscono l'una all'altra:

*Tabella studenti*

| student_id | name      |
| ---------- | --------- |
| 0          | Marco     |
| 1          | Francesco |
| 2          | Luigi     |
| 3          | Paolo     |

*Tabella voti*

| id  | vote | student_id_reference | subject    |
| --- | ---- | -------------------- | ---------- |
| 0   | 4    | 0                    | Matematica |
| 1   | 6    | 2                    | Italiano   |
| 2   | 8    | 0                    | Italiano   |
| 3   | 2    | 3                    | Storia     |

Formo i modelli

```pseudo-code
class student
{
	int id;
	string name;
}

class vote
{
	int id;
	int vote;
	int student_id_reference;
}
```

Formo i record

```pseudo-code
class student_situation
{
	private int _id;
	int name;

	int? voto_in_italiano;
	int? voto_in_matematica;
}
```

Formo la repository
```pseudo-code
class students_situations_repository
{
	database_context context;
	student[] students;
	vote[] votes;
	
	student_situation get_student_sitution(student_id) {
		student = student.find(id == student_id);
		vote[] students_votes = votes.find(student_id_reference == student.id);

		return new student_stuation() {
			name = student.name,
			voto_in_italiano = students_votes.find(subject == "italiano"),
			voto_in_matematica = students_votes.find(subject == "matematica")
		}
	}

	void store_vote(vote) {
		votes.add(vote);
		context.store();
	}
}
```

Il compito della repository è quello di confrontarsi con i modelli e collegare le varie informazioni per creare un oggetto o un comportamento di ritorno.