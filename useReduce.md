# useReduce

1. `{ useReducer }`
2. `const [count, dispatch] = useReducer(reducer, initialState)` pozivamo useReducer funkciju. Prihvata dva parametra
  * reducer funkciju
  * initialState
3. `onst initialState = 0` definišemo initialState
4. `const reducer = (state, action) => {` definišemo reducer funkciju. **Prihvata dve vrednosti a vraća jednu, novi satte**
  * state je trenutno stanje
  * action, u našem slučaju sabiranje, oduzimanje i reset.
5. `switch (action)`
6. `<button onClick={() => dispatch('increment')}>Increment</button>`

```jsx
import React, { useReducer } from 'react'

const initialState = 0 // <--- 3
const reducer = (state, action) => {
	switch (action) {
		case 'increment':
			return state + 1
		case 'decrement':
			return state - 1
		case 'reset':
			return initialState
		default:
			return state
	}
}

function CounterOne() {
	const [count, dispatch] = useReducer(reducer, initialState)

	return (
    <div>
      <div>Count = {count}</div>
      <button onClick={() => dispatch('increment')}>Increment</button>
			<button onClick={() => dispatch('decrement')}>Decrement</button>
			<button onClick={() => dispatch('reset')}>Reset</button>
		</div>
	)
}

export default CounterOne
```

# useReduce i objekti

1. `const initialState = 0` menjamo u objekat `const initialState = { firstCounter: 0,` i 
2. `<div>Count = {count}</div>` menjamo u `<div>Count = {count.firstCounter}</div>`
3. `dispatch('increment')` menjamo u `dispatch({ type: 'increment' }`
4. `switch (action)` menjamo u `switch (action.type)`
5. `return state + 1` <---> `return {firstCounter: state.firstCounter }`

1. Ako ovom kodu želimo dodati više dugmadi ali ovaj puta da uvećanje bude npr 5, postižemo lako
  * `dispatch({ type: 'increment' }` dodajemo `catch({ type: 'increment', value: 5 }`
  * `return {firstCounter: state.firstCounter }` dodajemo `return {firstCounter: state.firstCounter + action.value }`

1. Sledeći slučaj je kad u state dodajemo više elemenata
```jsx
const initialState = {
	firstCounter: 0,
	secondCounter: 10 // <-----*
  ```
2. `return { ...state, firstCounter: state.firstCounter + action.value }` dodajemo ...state jer imamo dva stejta.
3. `<div>Secound Counter = {count.secondCounter}</div>` dodajemo Secound counter u JSX.
4. Dodajemo dva nova dugmeta i menjamo dispatc u dispatch({ type: 'increment2', value: 1 })
 

```jsx
import React, { useReducer } from 'react'

const initialState = {
	firstCounter: 0,
	secondCounter: 10
}
const reducer = (state, action) => {
	switch (action.type) {
		case 'increment':
      // ...state smo dodali jer imamo dva initialState, + action.value jer sabiramo sa 1 ili 5
			return { ...state, firstCounter: state.firstCounter + action.value } 
		case 'decrement':
			return { ...state, firstCounter: state.firstCounter - action.value }
		case 'increment2':
			return { ...state, secondCounter: state.secondCounter + action.value }
		case 'decrement2':
			return { ...state, secondCounter: state.secondCounter - action.value }
		case 'reset':
			return initialState
		default:
			return state
	}
}

function CounterTwo() {
	const [count, dispatch] = useReducer(reducer, initialState)

	return (
		<div>
			<div>Count = {count.firstCounter}</div>
			<button onClick={() => dispatch({ type: 'increment', value: 1 })}>
				Increment
			</button>
			<button onClick={() => dispatch({ type: 'decrement', value: 1 })}>
				Decrement
			</button>
			<button onClick={() => dispatch({ type: 'increment', value: 5 })}>
				Increment 5
			</button>
			<button onClick={() => dispatch({ type: 'decrement', value: 5 })}>
				Decrement 5
			</button>
			<button onClick={() => dispatch({ type: 'reset' })}>Reset</button>
			<div>Secound Counter = {count.secondCounter}</div>
			<div>
				<button onClick={() => dispatch({ type: 'increment2', value: 1 })}>
					Increment
				</button>
				<button onClick={() => dispatch({ type: 'decrement2', value: 1 })}>
					Decrement
				</button>
			</div>
		</div>
	)
}

export default CounterTwo
```
# Multiple useReducers

koristimo da pojednostavimo prethodni primer

1. Dodajemo drugi useReducers `countTwo` i `dispatchTwo`
```jsx
const [count, dispatch] = useReducer(reducer, initialState)
	const [countTwo, dispatchTwo] = useReducer(reducer, initialState) // <---+
  ```
2. Samo dupliramo JSX kod. I ovde menjamo `{count}` u `{countTwo}`, `dispatch` u `dispatchTwo`


---
```jsx
import React, { useReducer } from 'react'

const initialState = 0
const reducer = (state, action) => {
	switch (action) {
		case 'increment':
			return state + 1
		case 'decrement':
			return state - 1
		case 'reset':
			return initialState
		default:
			return state
	}
}

function CounterThree() {
	const [count, dispatch] = useReducer(reducer, initialState)
	const [countTwo, dispatchTwo] = useReducer(reducer, initialState)

	return (
		<div>
			<div>Count = {count}</div>
			<button onClick={() => dispatch('increment')}>Increment</button>
			<button onClick={() => dispatch('decrement')}>Decrement</button>
			<button onClick={() => dispatch('reset')}>Reset</button>

			<div>Count = {countTwo}</div>
			<button onClick={() => dispatchTwo('increment')}>Increment</button>
			<button onClick={() => dispatchTwo('decrement')}>Decrement</button>
			<button onClick={() => dispatchTwo('reset')}>Reset</button>
		</div>
	)
}

export default CounterThree
```
