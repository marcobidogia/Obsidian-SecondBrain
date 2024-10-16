---
tags:
  - databases
  - sql
---

# Intro
([Tutorial republic](https://www.tutorialrepublic.com/sql-tutorial/))

Un database SQL è un tipo di database diviso in varie unità logiche chiamate tabelle.

# Sintassi

``` sql
-- query per recuperare dipendenti per stipendio oltre 1800
SELECT nome, data_assunzione, stipendio FROM dipendenti WHERE stipendio > 1800;
```

Gli *statements* SQL si leggono esattamente come si scrivono, in questo caso la query seleziona (SELECT) le proprietà "name, data_assunzione, stipendio" dalla tabella (FROM) "dipendenti", le quali righe hanno la proprietà stipendio maggiore di 1800 (WHERE).


> [!info] Best practise
> Per convenzione i campi di base della sintassi SQL devono essere scritti in MAIUSCOLO e lo statement deve finire con il carattere ";".

# Comandi
## Database
``` SQL
-- crea database
CREATE DATABASE <nome database>;

-- distrugge database
DROP DATABASE <nome database>;
```

## Tabelle
``` SQL
--crea tabaella
CREATE TABLE nometabella(
nome_campo tipo_di_dato constraint,
);

--esempio
CREATE TABLE prova(id int);

--cancella tabella
DROP TABLE prova;

--crea una tabella se non esiste già
CREATE TABLE IF NOT EXIST <nome tabella> (<nome dato> <tipo dato> <constaint>);
```

per i tipi di dati fare riferiemento a: [Tutorial republic -> Tipi di dati](https://www.tutorialrepublic.com/sql-tutorial/sql-create-table-statement.php)

## Constraint
``` sql
--esempio
CREATE TABLE prova(id int not null);
```

"not null" indica che il valore da aggiungere non deve essere nullo.

### Primary key
indica che il valore deve essere la chiave univoca del dato

``` sql
--esempio
CREATE TABLE prova(
id int not null,
PRIMARY KEY (id)
);
```

### Unique
Un campo univoco.

### Default
``` sql
--esempio
CREATE TABLE prova(
id int not null,
mansione_dipendente varchar(255) not null default "impiegato"
PRIMARY KEY (id)
);
```

indica che quando non viene specificato il valore di quella colonna verrà dato il valore "default".

### Check
``` sql
--esempio
CREATE TABLE prova(
id int not null,
mansione_dipendente varchar(255) not null default "impiegato",
stipendio int not null check (stipendio >= 1200 and stipendio <= 5000)
PRIMARY KEY (id)
);
```

fa in modo che quando verrà inserito il valore della colonna stipendio ci sara un controllo sul valore che stia all'interno del range inserito ad esempio.

### Foreign key
``` sql
--esempio
CREATE TABLE prova(
id int not null,
mansione_dipendente varchar(255) not null default "impiegato",
stipendio int not null check (stipendio >= 1200 and stipendio <= 5000)
PRIMARY KEY (id),
FOREIGN KEY (id) REFERENCES rapporto_clienti(id <nome su tabella rapporto_cliente>)
);
```

indica che il valore della colonna id sarà l'indice per la tabella rapporto per le ricerche.

### Insert
```sql
INSERT INTO <nome tabella> (<colonna1>, ...)
VALUES (<valore colonna 1>, ..)
```

### Select
```sql
SELECT <colonne che interessano divise da ,> FROM <nome>   
```

### Condizioni con where
```sql
SELECT <colonne desiderate> FROM <tabella> WHERE <condizione>   
```


- Uguaglianza o diversità: \<nome della colonna\> =\/!= \<valore\>
- Minore/Maggiore (o uguale) di: \<nome colonna\> >/< \<valore\>
- And/Or/Not: AND | OR | NOT
- IN: cerca all'interno del valore di una lista

``` sql
... WHERE mansione IN ('impiegato', 'commerciale')
```

- BETWEEN: cerca che il valore stia all'interno di due limiti

```sql
... WHERE valore BETWEEN min_value AND max_value   
```
- LIKE:
```sql
WHERE <prop> LIKE '%C'   
```

| Statement              | Meaning                                                                                               | Values Returned  |
| ---------------------- | ----------------------------------------------------------------------------------------------------- | ---------------- |
| WHERE name LIKE 'Da%'  | Find names beginning with _Da_                                                                        | David, Davidson  |
| WHERE name LIKE '%th'  | Find names ending with _th_                                                                           | Elizabeth, Smith |
| WHERE name LIKE '%on%' | Find names containing the _on_                                                                        | Davidson, Toni   |
| WHERE name LIKE 'Sa_'  | Find names beginning with _Sa_ and is followed by at most one character                               | Sam              |
| WHERE name LIKE '_oy'  | Find names ending with _oy_ and is preceded by at most one character                                  | Joy, Roy         |
| WHERE name LIKE '_an_' | Find names containing _an_ and begins and ends with at most one character                             | Dana, Hans       |
| WHERE name LIKE '%ar_' | Find names containing _ar_, begins with any number of characters, and ends with at most one character | Richard, Karl    |
| WHERE name LIKE '_ar%' | Find names containing _ar_, begins with at most one character, and ends with any number of characters | Karl, Mariya     |
Let's put the statements we've discussed above into real use by searching some records.
Consider we've an _employees_ table in our database with the following records:

``` sql
+--------+------------------+------------+--------+---------+
| emp_id | emp_name         | hire_date  | salary | dept_id |
+--------+------------------+------------+--------+---------+
|      1 | Ethan Hunt       | 2001-05-01 |   5000 |       4 |
|      2 | Tony Montana     | 2002-07-15 |   6500 |       1 |
|      3 | Sarah Connor     | 2005-10-18 |   8000 |       5 |
|      4 | Rick Deckard     | 2007-01-03 |   7200 |       3 |
|      5 | Martin Blank     | 2008-06-24 |   5600 |    NULL |
|      6 | simons bistro    | 2009-04-01 |   6000 |       1 |
+--------+------------------+------------+--------+---------+

```

### Ordinamento
```sql
... ORDER BY <proprietà> ASC|DES
```

### Limit
```sql
SELECT * FROM table LIMIT 100   
```

Estrae i dati limitandosi a restituire 100 valori

- Offset, aggiunge un offset al limite:

```sql
SELECT * FROM table LIMIT <offset>, 100   
```

## Disctinct
Restituisce solo i valori diversi della colonna, se ho alcuni variabili uguali li salta.

```sql
SELECT DISTINCT citta FROM clienti;   
```

Ritorna le città sempre diverse fra i clienti.

## Count
Se messo su un SELECT estrae il numero di valori che escono da una colonna:

```sql
SELECT COUNT(citta) FROM clienti;  
```

Ritorna la lunghezza lista di città.

## Update
Sintassi:

```sql
UPDATE <tabella> SET colonna1 = valore1 WHERE consizione   
```

Aggiorna la tabella, nella colonna 1 con il valore "valore1" a tutti gli oggetti che rispondono al where.

## Delete
Sintassi:

```sql
DELETE FROM tabella WHERE condizione;   
```

Cancella dalla tabella "tabella" usando la condizione "condizione"


> [!warning] 
> RICORDA LA CONDIZIONE! ALTRIMENTI VERRANNO CANCELLATI TUTTI I DATI

## Truncate
Ricrea la tabella aggiornando anche autoincrement

Sintassi:

```sql
TRUNCATE TABLE <nome tabella>
```

> TRUNCATE TABLE vs DELETE 
> Although DELETE and TRUNCATE TABLE seem to have the same effect, but they do work differently. Here are some major differences between these two statements: 
> - TRUNCATE TABLE statement drop and re-create the table in such a way that any auto-increment value is reset to its start value which is generally 1.
> - DELETE lets you filter which rows to be deleted based upon an optional WHERE clause, whereas TRUNCATE TABLE doesn't support WHERE clause it just removes all the rows. 
> - TRUNCATE TABLE is faster and uses fewer system resources than DELETE, because DELETE scans the table to generate a count of rows that were affected then delete the rows one by one and records an entry in the database log for each deleted row, while TRUNCATE TABLE just delete all the rows without providing any additional information.

## JOIN
[Tutorial republic -> JOIN](https://www.tutorialrepublic.com/sql-tutorial/sql-joining-tables.php)

### Inner Join
```sql
SELECT <cosa voglio tirare fuori sia da tabella 1 che da 2 es. tabella1.prop, tabella2.prop> FROM <tabella 1> INNER JOIN <tabella 2> ON <condizione tipo: tabella1.prop = tabella2.prop>
```

#### Left Join e Right Join
Collega tutta la tabella di di una parte e quello che matcha dell'altra