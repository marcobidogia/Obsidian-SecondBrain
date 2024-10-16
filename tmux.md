---
tags:
  - arch
  - linux
  - wiki
  - tmux
  - shortcuts
---

# Intro

Tmux e' un Terminal multiplexer, praticamente un terminale che contiene altri terminali.
I principali benefici sono la persistenza, session sharing multiwindows

---
# Shortcuts

Di default `<leader>` e' CTRL + b, l'ho reimpostato a CTRL + s

| Comando                   | Descrizione                                                            |
| ------------------------- | ---------------------------------------------------------------------- |
| `<leader>` + :            | Commmand mode                                                          |
| `<leader>` + c            | crea una nuova finestra                                                |
| `<leader>` + n (o numero) | ritorna sulla finestra precedente (o su quella del numero selezionato) |
| `<leader>` + %            | Split orizzontale                                                      |
| `<leader>` + "            | Split verticale                                                        |
| `<leader>` + Freccia      | Mi sposto tra le finestre                                              |
| `<leader>` + d            | detach dalla sessione                                                  |
| `<leader>` + s            | lista le sessioni e navigo con su e giu' enter per entrarci            |
| `<leader>` +              |                                                                        |
| `<leader>` +              |                                                                        |
| `<leader>` +              |                                                                        |
| `<leader>` +              |                                                                        |
|                           |                                                                        |

---
# Comandi in tmux

| Comando                | Descrizione                      |
| ---------------------- | -------------------------------- |
| rename-window `<name>` | rinomina la finestra selezionata |
| rename-session         | rinomina la sessione             |
|                        |                                  |

---
# Comandi fuori tmux

| Comando     | Descrizione                         |
| ----------- | ----------------------------------- |
| tmux        | crea una nuova sessione tmux        |
| tmux ls     | lista le sessioni in funzione       |
| tmux attach | si collega alla sessione precedente |
|             |                                     |

