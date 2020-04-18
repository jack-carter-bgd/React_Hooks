# useRef
Sa useRef možemo direktno da pristupimo DOM Nodes. Najviše se upotrebljava za fokusiranje ligin forme, npr. username.

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
