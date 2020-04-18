# useRef
Sa useRef možemo direktno da pristupimo DOM Nodes. Koristimo ga npr. za fokusiranje username u ligin forme.
1. Uvezemo { useRef, useEffect }.
2. Unutar funkcije pozivamo useEffect. useEffect prihvata arrow function ( ) => { }  i dependency array [ ]. Ostavljamo [] prazan jer želimo da funkciju pokrenemo samo jednom. 
```jsx
useEffect(() => {
    
  }, [])
```
3. Previmo Ref varijablu i dodeljujemo inicijalnu vrednost (null)
```jsx
const inputRef = useRef(null)
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
