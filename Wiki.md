---
tags:
  - coding
  - javascript
  - typescrypt
  - react
  - software_design
---
# Hooks


## State
Sono tutti gli hooks di stato che servono a "ricordare dei valori"

### [useState](https://react.dev/reference/react/useState)
Dichiara una variabile che puoi direttamente aggiornare
```javascript
function ImageGallery() {  
	const [index, setIndex] = useState(0);  
	// ...
```

### [useReducer](https://react.dev/reference/react/useReducer)
Dichiara una variabile con delle logiche di aggiornamento
```javascript
import { useReducer } from 'react';

function reducer(state, action) {
  // ...
}

function MyComponent() {
  const [state, dispatch] = useReducer(reducer, { age: 42 });
  // ...

function reducer(state, action) {
  switch (action.type) {
    case 'incremented_age': {
      // ✅ Correct: creating a new object
      return {
        ...state,
        age: state.age + 1
      };
    }
    case 'changed_name': {
      // ✅ Correct: creating a new object
      return {
        ...state,
        name: action.nextName
      };
    }
    // ...
  }
}
```

## Context
É l'hook che riceve le informazioni da un parente distante senza passarlo come proprietá all'interno del componente stesso, ad esempio il tema scuro o chiaro dell'UI.

### [useContext](https://react.dev/reference/react/useContext)
Legge e si iscrive al contesto.

```javascript
function Button() {  
	const theme = useContext(ThemeContext);  
	// ...
```

## Ref
Ref permette ad un componente di manttenere delle informazioni che non sono usante per il rendering, come il nodo DOM o il Timeout ID.
Diversamente dagli stati ref non renderizza nuovamente il componente

### [useRef](https://react.dev/reference/react/useRef)
É un modo per dichiarare un ref, é possibile aggiungere qualsiasi cosa come suo valore ma molto spesso viene usato per mantenere il nodo del DOM. 
```javascript
import { useRef } from 'react';

function MyComponent() {
  const intervalRef = useRef(0);
  const inputRef = useRef(null);
  // ...
```

### [useImperativeHandle](https://react.dev/reference/react/useImperativeHandle)
Aiuta a customizzare i riferimenti esposti dai componenti.
```javascript
import { forwardRef, useImperativeHandle } from 'react';

const MyInput = forwardRef(function MyInput(props, ref) {
  useImperativeHandle(ref, () => {
    return {
      // ... your methods ...
    };
  }, []);
  // ...
```

## Effect
Gli effetti sono per un componente il modo di connettersi e sincronizzarsi a sistemi esterni.

### [useEffect](https://react.dev/reference/react/useEffect#)
Connette il componente ad un sistema esterno

```javascript
function ChatRoom({ roomId }) {
  useEffect(() => {
    const connection = createConnection(roomId);
    connection.connect();
    return () => connection.disconnect();
  }, [roomId]);
  // ...
```
