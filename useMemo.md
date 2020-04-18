# useMemo useCallback

## useMemo


> Kad želimo da keširamo funkciju koristimo callBack a kad želimo da keširamo rezultat koristimo useMemo.useCallback kešira instancu funkcije dok useMemo poosle inicijalnog pozivanja funkcije kešira rezultat. 

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

## useCallback

> usaCallback vraća memoized verziju callback funkcije koja će se jedino menjati ako joj se dependecies promeni. Koristimo kada proselđujemo callbacks da optimizujemo child components, koje smo optimizivali sa  `export default React.memo(Button)` da sprečimo nepotrebno rirenderovanje. Keširamo funkciju i prosleđujemo je kao props.

Umesto
```jxs
const increment = (() => {
  setCount(count + 1)
})
```
kositimo
```jsx
const increment = useCallback(() => {
  setCount(count + 1)
}, [count])
```
---

```jsx
import React, { useState, useCallback } from 'react'
import Count from './Count'
import Button from './Button'
import Title from './Title'

function ParentComponent() {
	const [age, setAge] = useState(25)
	const [salary, setSalary] = useState(50000)

	const incrementAge = useCallback(() => {
		setAge(age + 1)
	}, [age])

	const incrementSalary = useCallback(() => {
		setSalary(salary + 1000)
	}, [salary])

	return (
		<div>
			<Title />
			<Count text="Age" count={age} />
			<Button handleClick={incrementAge}>Increment Age</Button>
			<Count text="Salary" count={salary} />
			<Button handleClick={incrementSalary}>Increment Salary</Button>
		</div>
	)
}

export default ParentComponent
```
