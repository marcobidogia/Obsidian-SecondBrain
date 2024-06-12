---
tags:
  - programming_languages
  - python
  - virtualizzation
---
Arch Linux gestisce i pacchetti Python in modo tale da evitare conflitti con il sistema di gestione dei pacchetti del sistema operativo. La soluzione raccomandata è quella di utilizzare un ambiente virtuale per installare pacchetti Python specifici per progetto.

Ecco i passaggi per creare un ambiente virtuale e installare `pymongo` all'interno di esso:

### 1. Creazione di un Ambiente Virtuale

1. **Assicurati di avere `python-virtualenv` installato:**
   ```bash
   sudo pacman -S python-virtualenv
   ```

2. **Crea un ambiente virtuale:**
   ```bash
   python -m venv myenv
   ```
   Questo creerà una directory chiamata `myenv` nella cartella corrente. Puoi sostituire `myenv` con qualsiasi nome preferisci.

### 2. Attivazione dell'Ambiente Virtuale

1. **Attiva l'ambiente virtuale:**
   ```bash
   source myenv/bin/activate
   ```
   Il prompt del terminale cambierà per indicare che l'ambiente virtuale è attivo.

### 3. Installazione di `pymongo`

1. **Installa `pymongo` nell'ambiente virtuale attivo:**
   ```bash
   pip install pymongo
   ```

### 4. Utilizzo dell'Ambiente Virtuale

1. **Scrivi e esegui i tuoi script Python all'interno dell'ambiente virtuale:**
   Ad esempio, puoi creare un file `test.py`:
   ```python
   from pymongo import MongoClient

   client = MongoClient("mongodb://localhost:27017/")
   print(client.list_database_names())
   ```

2. **Esegui il tuo script:**
   ```bash
   python test.py
   ```

### 5. Disattivazione dell'Ambiente Virtuale

1. **Quando hai finito, disattiva l'ambiente virtuale:**
   ```bash
   deactivate
   ```

### Riassunto dei Comandi

Ecco una serie di comandi che puoi copiare e incollare nel terminale per eseguire tutti i passaggi sopra descritti:

```bash
# Assicurati di avere virtualenv installato
sudo pacman -S python-virtualenv

# Crea un ambiente virtuale
python -m venv myenv

# Attiva l'ambiente virtuale
source myenv/bin/activate

# Installa pymongo
pip install pymongo

# Verifica l'installazione di pymongo
pip list

# Disattiva l'ambiente virtuale quando hai finito
deactivate
```

Questo approccio ti consente di gestire le dipendenze del progetto senza influenzare il sistema globale e ti permette di evitare conflitti con il sistema di gestione dei pacchetti di Arch Linux.