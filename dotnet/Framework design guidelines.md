---
tags:
  - dotnet
  - guidelines
---
# Naming Guidelines
Sotto delle convenzioni di come scrivere i nomi.
## Capitalization conventions
Pascal case: Prima lettera maiuscola e per ogni nuova parola una lettera maiuscola: `VariableName`
Camel case: Prima lettera minuscola e per ogni nuova parola una lettera maiuscola: `variableName`

| Identifier | Casing | Example                                                                                                                                                                   |
| ---------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Namespace  | Pascal | `namespace System.Security { ... }`                                                                                                                                       |
| Type       | Pascal | `public class StreamReader { ... }`                                                                                                                                       |
| Interface  | Pascal | `public interface IEnumerable { ... }`                                                                                                                                    |
| Method     | Pascal | `public class Object {`  <br>`public virtual string ToString();`  <br>`}`                                                                                                 |
| Property   | Pascal | `public class String {`  <br>`public int Length { get; }`  <br>`}`                                                                                                        |
| Event      | Pascal | `public class Process {`  <br>`public event EventHandler Exited;`  <br>`}`                                                                                                |
| Field      | Pascal | `public class MessageQueue {`  <br>`public static readonly TimeSpan`  <br>`InfiniteTimeout;`  <br>`}`  <br>`public struct UInt32 {`  <br>`public const Min = 0;`  <br>`}` |
| Enum value | Pascal | `public enum FileMode {`  <br>`Append,`  <br>`...`  <br>`}`                                                                                                               |
| Parameter  | Camel  | `public class Convert {`  <br>`public static int ToInt32(string value);`  <br>`}`                                                                                         |

## General conventions

- Scegliere quando si puó un nome leggibile.
- Preferire la leggibilitá alla brevitá.
- NON usare undescore, trattini, ogni non carattere non numerico.
- NON usare la [notazione Ungara](https://en.wikipedia.org/wiki/Hungarian_notation).
- EVITARE identificatori che possono creare conflitti.
- NON usare abbreviazioni o acronimi.
- usare nomi comuni.
- usare nomi simili alle vecchie api se riscritte in nuove versioni.
- preferire di aggiungere un suffisso piuttosto che un prefisso nella nuova versione dell'api.
- considerare di unsare un nuovo brand piuttosto di aggiungere un suffisso o prefisso.
- NON usare il prefisso "Ex" o similari
- usare il sufisso 64 introducendo versioni di api che operano a 64 bit.

## Names of Assemblies and DLLs

- Scegliere nomi per gli assempli che comprendalo larghi chunk di funzionalitá
- Considerare nomi che seguano il seguente pattern `<Company>.<Component>.dll`

## Names of Namespaces
`<Company>.(<Product>|<Technology>)[.<Feature>][.<Subnamespace>]`

- usare come prefisso il nome della compagnia per evitare namespace simili.
- usare il nome di versione indipendente sul secondo livello del namespace.
- NON usare la gerarchie organizatoriali.
- usare il Pascal Casing.
- Considerare il plurale se appropiato.
- NON usare lo stesso nome per namespace e tipo di namespace.
- NON usare termini generici.

## Names of Classes, Structs, and Interfaces
