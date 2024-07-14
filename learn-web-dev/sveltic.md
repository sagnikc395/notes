---
title: Making a Svelte Compiler
tags:
  - svelte
  - compilers
  - web-dev
date: 12/7/24
---
### Basics:
- React makes easy to describe complex UIs easily but is not performant enough.
- Svelte since it is compiled into DOM level Javascript before being developed, uses the optimized approach.
- Svelte is a compiler based framework
	- takes the code and transforms into DOM.
- How do we build our own Svelte ? 
	- figure that out together.

- Svelte Compiler:
	- Takes our code ->
		- parses out code into a tree structure -> AST structure.
		- The code is Abstract from the JS code instead of a concrete implementation.
	- AST is analyzed and get information like:
		- Variables
		- what state changes.
	- Generate the DOM code required for that.

- app.mjs :
	- read the content from app.svelte from fs.
	- generate the ast from the content by **parsing** it.
	- analysis of the ast using the **analyzer**
	- and then generate the js output using the generate method. 

- How does the optimized Javascript looks like ?
	- wrap the button and wrap inside a objec tlifecycle, to make it generic enough and to create and destory at ease.
	- we will wrap this around a create method for that 
```svelte
	<script>
		let counter = 0;
		const increment = () => counter++;
		const decrement = () => decrement--;
	</script>
<button on:click={decerement}>Decrement</button>
<div>{counter}</div>
<button on:click={increment}>Increment</button>
```
- can we wrapped aorund a lifecycle object and called inside an App function as:
```js
function App(){
	let button;
	const lifecycle = {
		create(target){
			button = document.createElement('button');
			button.addEventListener('click',decrement);
			target.appendChild(button);
			//adding text to the button 
			text = document.createTextNode('Decrement');
			button.appendChild(text);
			//...
		},
		//need a lifecycle method called update(), that will be dynamic and update the counter variable 
		update(changed){
			if(changed.includes("counter")){
				text2.data = counter;
			}
		},
		destroy(){
		button.removeEventListener('click',decrement);
		target.removeChild(button);
		}
	};
return lifecycle;
}

App().create(document.body);
```
- So we can create new components for this lifecycles
- to know {counter} is dynamic we need to analyze the code and to transform it.


- At the end of day, svelte code is just string -> need to parse into strings, simply going through code one by one, is simplify going through the code in an AST.


### Syntax Notation:
- design document for the syntax.
- various syntax notation like railroad diagram and backus-naur form.
- "Svelte" Syntax:
```bnf 
<fragments> ::== <fragment> | <fragment> <fragment>
<fragment> ::== <script> | <element> | <expression> | <text>
<script> ::== "<script>" <javascript> "</script>"
<element> ::= "<" <tag-name> <attribute-list> ">" <fragments> "</" <tag-name> ">"
<attribute-list> ::= | <space> <attribute> | <attribute-list> <space> <attribute>
<attribute> ::= <attribute-name> "={" <javascript> "}"
<expression> ::= "{" <javascript> "}"
```

### Parsing Code:
- i is the pointer and points to the current character we are parsing for.
- write 3 helper functions for us to :
	- match what i is pointing at -> match()
	- advance i -> eat()
	- read what value i is pointing at -> 