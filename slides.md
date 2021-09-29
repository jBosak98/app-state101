# Application state and how to fight with it



###### Jakub Bosak

---

## Fight with the application state

---

## Pure functions

---

## Pure functions

* lack of side effects
* idempotence

----

## Side effects
```js
let counter = 1;
const increment = () => counter++;
...
increment();

```

----

## Idempotence
```js
Math.random();
```

----

## Idempotence
```js
let counter = 1;
const increment = () => counter++;
...
increment();

```

---


## But we need a state ☹️

---

## How to manage state?
React useState!

```js
import React, { useState } from 'react';

const Foo = () => {
  const [counter, setCounter] = useState(0);
  const onClick = () => setCounter(oldState => oldState+1);
  return <>
      <button onClick={onClick}>
        CLICK
      </button>
  </>
}
```

---


## How to manage state?
React context!

```js
const CounterContext = React.createContext();

const CountProvider = ({children}) => {

  const [counter, setCounter] = React.useState(0);
  const increase = () => setCounter(prevState=>prevState + 1);
  const value = { counter, setCounter, increase };
  return <CountContext.Provider value={value}>
    {children}
  </CountContext.Provider>

}
```

---

## How to manage state?
React context!

```js
const useCounter = () => {
  const context = React.useContext(CounterContext);

  if (context === undefined) {
    throw new Error('useCount must be used within a CountProvider')
  }

  return context;
}
const Foo = () => {
  const { counter, increase } = useCounter;
  return <button onClick={increase}>{counter}</button>
}
```
---

## How to manage state?
Zustand!

```js
import create from "zustand";

const useStore = create((set) => ({
  counter: 1,
  increase: () => set((state) => ({
    counter: state.counter + 1
  })),
}));

export default useStore;
```

---
## How to manage state?
Zustand!

```js

const Foo = () => {
    const { counter, increase } = useStore((state) => state);
    return <button onClick={increase}>{counter}</button>

};
export default useStore;
```

---
## Now you're ready to write an application state :)
---

## any questions?

---
### resources:
* https://blog.alyssaholland.me/pure-functions-in-javascript
* https://blog.bitsrc.io/zustands-guide-to-simple-state-management-12c654c69990
* https://kentcdodds.com/blog/how-to-use-react-context-effectively