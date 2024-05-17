---
tags:
  - databases
  - sql
---

# Intro

Un database SQL è un tipo di database diviso in varie unità logiche chiamate tabelle.

# Sintassi

``` sql
-- query per recuperare dipendenti per stipendio oltre 1800
SELECT nome, data_assunzione, stipendio FROM dipendenti WHERE stipendio > 1800;
```

Gli *statements* SQL si leggono esattamente come si scrivono, in questo caso la query seleziona (SELECT) le proprietà "name, data_assunzione, stipendio" dalla tabella (FROM) "dipendenti", le quali righe hanno la proprietà stipendio maggiore di 1800 (WHERE).

