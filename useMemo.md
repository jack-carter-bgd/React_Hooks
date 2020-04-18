# useMemo useCallback

useCallback kešira instancu funkcije dok useMemo poziva funkciju i kešira rezultat. 

> Kad želimo da keširamo funkciju koristimo callBack a kad želimo da keširamo rezultat koristimo useMemo.

Se koristi za optimizaciju brzine tako što koristi keš i izbegava renderovanje tamo gde nije potrebno sve kod se dependecies vrednost ne promeni. U sledećem primeru se svaki put izvršava `while (i < 2000000000) i++` kod iako do promene nije došlo.

1. Uvozimo `{ useState, useMemo }`
2. Pozivamo `useMemo()` i kao prvi arument dajemo funkciju čiji return treba da se kešira (u našem slučaju funkcija koja proverava da li je broj paran ili neparan)
3. Kao drugi parametar definišeno Dependencies, u našem slučaju [counterOne]. Koristimo keš memoruiju pri renderovanju sem sako se [counterOne] vrednost promeni.
4. `<span>{isEven ? 'Even' : 'Odd'}</span>`
```jsx
import React, { useState, useMemo } from 'react' // <--- 1

function Counter() {
	const [counterOne, setCounterOne] = useState(0)
	const [counterTwo, setCounterTwo] = useState(0)

	const incrementOne = () => {
		setCounterOne(counterOne + 1)
	}

	const incrementTwo = () => {
		setCounterTwo(counterTwo + 1)
  }

  const isEven = useMemo(() => { // <--- 2
    let i = 0
    while (i < 2000000000) i++
    return counterOne % 2 === 0
  }, [counterOne]) // <--- 3

	return (
		<div>
			<div>
        <button onClick={incrementOne}>Count One - {counterOne}</button>
        <span>{isEven ? 'Even' : 'Odd'}</span>
			</div>
			<div>
        <button onClick={incrementTwo}>Count Two - {counterTwo}</button>
			</div>
		</div>
	)
}

export default Counter
```
