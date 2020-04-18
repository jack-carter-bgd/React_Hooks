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
## Ceo kod

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
