---
tags:
  - coding
  - course
---

## Mocha
Mocha è uno dei pacchetti usati per testare il codice Javascript.
Per installarlo sarà semplicemente necessario:
```bash
npm init             #se non è già stato eseguito
npm install mocha -D
```

> [!Info]
> Here’s what this command means:
> - *npm install* tells npm to install a package from the internet and any other packages it depends on
> - *mocha* is the package you want to download
> - *-D* signifies that this package is a development dependency and will show up under the *devDependecies* section in package.json. This means that the package will only be included in development mode and will not be included in the production bundle.

in seguito la struttura del progetto sarà:

a seguito dell'installazione sarà possibile eseguire mocha in due modi:
1. Aggiungere Mocha ai node modules (non molto raccomandato) *$ ./node_modules/mocha/bin/mocha*
2. Aggiungere Mocha al package.json del progetto, all'interno di "scripts" è possibile aggiungere il riferimento "test:mocha"

```json
"scripts": {  
  "test": "mocha"  
}
```

Così facendo sarà possibile richiamare il comando *npm test*.