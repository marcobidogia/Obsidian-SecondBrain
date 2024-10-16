---
tags:
  - design_patterns
---
## Intent

**Factory Method** is a creational design pattern that provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created.

# Contesto
Il Factory Method é un design pattern che, come suggerisce il nome, rimpiazza la creazione di classi classica `new` e si specializza a farlo in modo autonomo.
Esempio:
![[./media/Pasted image 20240826111557.png|Pasted image 20240826111557.png]]

Nell'esempio di sopra la classe `Logistics` gestisce la funzione di `planDelivery()` che presumibilmente crea un trasporto dalle classi sotto le quali hanno la stessa funzione esposta `createTransport()`

Struttura: 
![[./media/Pasted image 20240826111812.png|Pasted image 20240826111812.png]]