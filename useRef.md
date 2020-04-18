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

1. Importovanje `{useState, useEffect, useRef}`
2. Kreiramo State varijablu ` const [timer, setTimer] = useState(0)`
3. useEffect  `setInterval`
```jsx
setInterval(() => {
setTimer(timer => timer + 1)
}, 1000)
```
4. 


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
eyJoaXN0b3J5IjpbLTkyMjUzMTI5NSwtNTkwMDE5NjcwLDE5Nz
k1ODc4MDZdfQ==
-->