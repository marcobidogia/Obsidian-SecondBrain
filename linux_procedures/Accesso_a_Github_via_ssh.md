---
tags:
  - linux_procedures
---

Per accedere a [[Github]] via ssh per impostare la connessione permanente da un server Linux è necessario seguire questa procedura:

1. Recati sulla cartella '/home/.ssh'

``` bash
 cd ~/.ssh
```

2. Crea il file rsa da importare in Github e stampalo a schermo

``` bash
 ssh-keygen -f <il_nome_che_vuoi>
 cat <il_nome_che_vuoi>.pub
```

3. Recati sul browser, pagina di [Github](https://github.com) e sul tuo account vai in Impostazioni -> SSH and GPG keys.
	In SSH keys premi "New SSH key"; inserisci nel box più grande il risultato dell'ultimo comando inviato e il nome che desideri.

Fatto!

> [!WARNING] Ricordati
> Ricorda di scaricare le directory via SSH e non via HTTPS.
