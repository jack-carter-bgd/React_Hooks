# useRef

Sa useRef možemo direktno da pristupimo DOM Nodes. Koristimo ga npr. za fokusiranje username u ligin forme.
1. Uvezemo `{ useRef, useEffect }`.
2. Unutar funkcije pozivamo useEffect. 
	* useEffect prihvata arrow function ( ) => { }  i 
	* dependency array [ ]. Arraz ostavljamo prazan jer želimo da funkciju pokrenemo samo jednom. 
```jsx
useEffect(() => {
    
  }, [])
```
3. Previmo Ref varijablu i dodeljujemo inicijalnu vrednost (null)
```jsx
const inputRef = useRef(null)
```
4. Povezujemo sa input elementom koristeći `ref = { }` atribut i imenom varijeble inputRef.
```jsx
<input ref={inputRef} type="text" />
```
5. Posledji korak pozvanje `focus()` metoda na input elementom.
```jsx
inputRef.current.focus()
```

```jsx
import React, { useRef, useEffect } from 'react'

function FocusInput() {
	const inputRef = useRef(null)
	useEffect(() => {
		inputRef.current.focus()
	}, [])
	return (
		<div>
			<input ref={inputRef} type="text" />
		</div>
	)
}

export default FocusInput
```

## setInterval, clearInterval
[codevolution](https://www.youtube.com/watch?v=LWg0OyZQffc&list=PLC3y8-rFHvwgg3vaYJgHGnModB54rxOk3&index=72)

1. Importovanje `{useState, useEffect, useRef}`
2. Kreiramo State varijablu 
```jsx 
const [timer, setTimer] = useState(0)
```
4. `useEffect` gde postavljamo `setInterval` i `clearInterval`
```jsx
setInterval(() => {
setTimer(timer => timer + 1)
}, 1000)
```
```jsx
return () => {
clearInterval(interValRef.current)
```
5. Resetujemo tajmer na dugme, ali sledeći kod neće raditi jer varijabla interval je definisana u useEffect i nije dostupna ovde. Zato koristimo useRef
```jsx 
<button onClick={() => clearInterval(interval)
```
> useRef pored toga što može da ima referencu na dom node, koristeći ref atribut, takođe može smeštati mutable value. Korisno je da neće dolaziti do novog renderovanja kad se vrednost promeni i vrednost će se sačunati i posle renderovanja.
6. Pravimo ref varijablu 
```jsx 
const interValRef = useRef()
```
7. Menjamo varijablu u `setInterval`, `clearInterval` i `onClick` 
```jsx
interValRef.current = setInterval(()
clearInterval(interValRef.current)
onClick={() => clearInterval(interValRef.current)
```
8. 
```jsx

```

```jsx
import React, {useState, useEffect, useRef} from 'react'

function HookTimer() {
  const [timer, setTimer] = useState(0)
  const interValRef = useRef()
  useEffect(() => {
    interValRef.current = setInterval(() => {
      setTimer(timer => timer + 1)
    }, 1000)
    return () => {
      clearInterval(interValRef.current)
    }
  }, [])
  return (
    <div>
      HookTimer - {timer} -
      <button onClick={() => clearInterval(interValRef.current)}>Clear Timer</button>
    </div>
  )
}

export default HookTimer
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQzMjY5MTk1OSwtNTkwMDE5NjcwLDE5Nz
k1ODc4MDZdfQ==
-->