---
tags:
  - nodejs
  - npm
  - javascript
  - typescrypt
---
# Configuazione
I pacchetti npm possono essere recuperati anche da custom npm registry. Una di queste é quella di [Github](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-npm-registry), Github Packages. Il problema principale nel usare questa repo é che per recuperare i pacchetti privati sará necessario configurare il proprio pc.

Ecco i comandi per farlo:
```powershell
npm config set @<your-account/org>:registry=https://npm.pkg.github.com
npm login --scope=<your-account/org> --auth-type=legacy --registry=https://npm.pkg.github.com
Username: <il tuo username>
Password: <Genera un token da Github>
```

Dopo aver configurato tutto é possibile agire sui pacchetti.

---
# Pubblicazione
## CLI
Esistono vari modi per pubblicare pacchetti via CLI, eccone alcuni:

### Package.json
Sul file di configurazione `package.json` é necessario apportare le seguenti modifiche:

```json 
./package.json

{
	"name": "@<your-uname/org>/<package-name>", //solo con questo formato.
	"private": false,                           //da impostare a false se a true
	"publishConfig":                            
	{
	    "registry": "https://npm.pkg.github.com"
	},
	"repository": 
	{
	    "type": "git",
	    "url": "<...url...>.git"
	}
	//...
}

```

> In maniera simile a .gitignore, é possibile aggiungere un file di configurazione chiamato `.npmignore` per ignorare dei file alla pubblicazione.

### Github Actions
... todo

---
# Recupero

Dopo aver avviato i comandi del paragrafo [[Publish npm package on GitHub#Configuazione]] é possible importare la libreria grazie al comando:

``` powershell
npm install @<uname/org>/<package-name>
```