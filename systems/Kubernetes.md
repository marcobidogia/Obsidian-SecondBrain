---
tags:
  - systems
---

## Intro
Kubernetes è un orchestratore di container, può essere installato in istanza singola o in più computer che costituiranno insieme un cluster.

Il compito di Kubernetes è quello di adempiere alle richieste di avviare container diversi e gestirne il load balancing tra le macchine. Esistono 2 installer di Kubernetes, k8s, più completo, k3s più leggero e ottimizzato per i dispositivi edge.

Un ottimo tool di controllo del cluster è Rancher, il quale espone un interfaccia grafica semplice per effettuare analisi e debug.

## Nomenclatura
- _node_ indica il singolo computer. Questo può essere _master_ o _worker_.
- _master_ indica il nodo che orchestra l'avvio di processi fra i vari _worker_. Il nodo _master_ può essere a sua volta un _worker_.
- _worker_ indica il nodo "lavoratore" sul quale verrà avviato il processo deciso dal master.

## Installazione (k3s)
Comincerò l'installazione dal nodo master utilizzando k3s.

### Nodo master
I comandi da inviare sono i seguenti:

``` bash
curl -sfL https://get.k3s.io | K3S_KUBECONFIG_MODE="664" sh -s kubectl version
```

Con *kubectl* sarà possibile verificare la corretta installazione del software.

Dopo un po' di tempo, circa 5 minuti sarà possibile avviare anche il seguente comando per verificare la corretta installazione:

```bash
kubectl get nodes  # output corretto # NAME    STATUS   ROLES                  AGE   VERSION # xxxxx   Ready    control-plane,master   54m   v1.28.7+k3s1   
```
