---
tags:
  - electron
  - javascript
  - react
link: 
---
Electron é un sistema multiprocesso basato su [Chromium](https://www.google.com/googlebooks/chrome/small_00.html), che fa da framework architetturale simile ai moderni browser.
# Modello del processo
Electron funziona in modo analogo ad una pagina di un browser, esistono due parti:
- Main process: la parte principale, simile al backend dell'applicazione costruita in Node Js e che ne espone le api.
- Render process: la parte che renderizza il frontend dell'applicazione.

## Main process
Questo processo ha i compiti di:

### Window management
Il main process deve generare le finestre di applicazione, le `BrowserWindow` per interagire con le finestre é possibile chiamare la proprietá `webContents`.

main.js
``` javascript
const { BrowserWindow } = require('electron')

const win = new BrowserWindow({ width: 800, height: 1500 })
win.loadURL('https://github.com')

const contents = win.webContents
console.log(contents)
```

> Note: A renderer process is also created for [web embeds](https://www.electronjs.org/docs/latest/tutorial/web-embeds) such as the `BrowserView` module. The `webContents` object is also accessible for embedded web content.

La finestra BrowserWindow é un modulo di EventEmitter che puó fungere da emettitore di eventi dell'utente.

Quando l'istanza di BrowserWindow viene distrutta anche il render process di quella termina.

### Application lifecycle
Ha il compito di getstire il ciclo di vita dell'applicazione. Un esempio é quello di chiudere l'applicazione quando tutte le pagine sono chiuse:

```javascript
// quitting the app when no windows are open on non-macOS platforms
app.on('window-all-closed', () => {
  if (process.platform !== 'darwin') app.quit()
})
```

### Native API's

Per estendere le funzinalitá puó aggiungere delle api custom.

---
## Processo di render

Electron per ogni `BrowserWindow` genera anche un processo di render. 
Ogni processo di render deve avere:
- un file HTML come entry point
- un file di stile CSS
- un file di script Javascript

Questo vuol dire che il processo di render non ha l'accesso ai componenti `required` da NodeJS e che questi devono essere importato con una specie di toolchain come nel browser.

### Preload scripts
Nell'istanza di `BroswerWindow` é possibile impostare nella proprietá `Preference` uno script che verrá caricato prima del HTML.

```javascript
const { BrowserWindow } = require('electron')  
// ...  
const win = new BrowserWindow({  
	webPreferences: {  
		preload: 'path/to/preload.js'  
	}  
})  
// ...
```

Normalmente in questi file sono presenti le informazioni di come si deve comportare l'applicazione.

```javascript
window.myAPI = {  
	desktop: true  
}
```

Questa parte del codice ha accesso anche al main process e quindi viene normalmente utilizzato come scambio di dati tra i due.
Comunque non é possibile agganciare delle variabili o procedure al preload process per impostazione predefinita del `contextIsolation`.
`contextIsolation` vuol dire che la parte di preload e quella di render sono isolate per evitare modifiche non desiderate dei privilegi delle API.

É possibile usare `contextBridge` peró per passare questo limite.
es. 

preload.js
```javascript
const { contextBridge } = require('electron')  
  
contextBridge.exposeInMainWorld('myAPI', {  
desktop: true  
})
```

render.js
```javascript
console.log(window.myAPI)
// => { desktop: true }
```

> This feature is incredibly useful for two main purposes:
> - By exposing [`ipcRenderer`](https://www.electronjs.org/docs/latest/api/ipc-renderer) helpers to the renderer, you can use inter-process communication (IPC) to trigger main process tasks from the renderer (and vice-versa).
> - If you're developing an Electron wrapper for an existing web app hosted on a remote URL, you can add custom properties onto the renderer's `window` global that can be used for desktop-only logic on the web client's side.

### The utility process
L'API UtilityProcess in Electron consente a un'app di generare più processi figli dal processo principale. Questi processi figli operano in un ambiente Node.js, quindi possono richiedere moduli e utilizzare tutte le API di Node.js.
L'UtilityProcess è utile per ospitare servizi non affidabili, attività che richiedono molta CPU o componenti soggetti a crash, che in precedenza sarebbero stati eseguiti nel processo principale o attraverso l'API `child_process.fork` di Node.js.
La principale differenza rispetto all'uso di `child_process.fork` è che l'UtilityProcess può stabilire un canale di comunicazione con un processo renderer tramite MessagePorts. Pertanto, è preferibile usare l'API UtilityProcess invece di `child_process.fork` quando è necessario generare un processo figlio dal processo principale.

### Process-specific module aliases (TypeScript)
Electron's npm package also exports subpaths that contain a subset of Electron's TypeScript type definitions.

- `electron/main` includes types for all main process modules.
- `electron/renderer` includes types for all renderer process modules.
- `electron/common` includes types for modules that can run in main and renderer processes.

These aliases have no impact on runtime, but can be used for typechecking and autocomplete.

Usage example

```javascript 
const { app } = require('electron/main')
const { shell } = require('electron/common')
```

## [Quick start](https://www.electronjs.org/docs/latest/tutorial/quick-start)
