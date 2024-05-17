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

