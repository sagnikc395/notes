---
title: Basics of Svelte
tags:
  - web-dev
  - svelte
---
## Basics:

### what is svelte ?
- Svelte is a JS framework like React and Vue, which share a goal of making it easy to build slick interactive user interfaces.
- Svelte converts our app into ideal JS at build time, rather than interpreting our application code at run time. This means we dont pay the performance cost of the framework's abstractions, and we don't encounter a penalty when our app first loads.

### components in svelte:
- In Svelte, an application is composed from one or more components.
- A component is a reusable self-contained block of code that encapsulates HTML,CSS and JS that belong together, written into a .svelte file. 
- A component can render data as well as it can encapsulate another value ,like a JS variable which we can write inside the script tag.
- in the tag we can also write JS expressions inside the curly braces, and also control element attributes, just like we use them to control text.
- Svelte compiler does a good job about reminding by making us accessible components that can be useful for other people in need ,like alt attribute in img tag.
- If the name and value of the attribute is the same , we can use shorthand and use the name as attribute.

### styling:
- just like HTML, we can add a style tag to our component inside our svelte files.
- These rules are scoped locally to the component, making it much easier to change styles.

### Nested Components:
- we can import components from other files and then use them as though we were including elements. use as 
 ```svelte
<script>
	import Nested from './Nested.svelte';
</script>
```
- For user defined components, we use captialized names.
- Also the styles dont leak in and are locally scoped.

## Reactivity:
- At the heart of Svelte there is a powerful system of reactivity for keeping the DOM in sync with our application state -> eg: in response to a event.
- Event Handler in svelte for clicking buttons:
```svelte 
<button on:click={incrementCounter}>Click Me!</button>

<!-- and the corresponding event handler in the script tag -->
<script>
let count = 0;

function incrementCouter() {
	count += 1;
	console.log(`Current count is ${count}`);
}
</script>
```
- Svelte will instrument this assignment with some code that will tell the DOM what needs to be updated.

### Declarations:
- Svelte's reactivity not only keeps the DOM in sync with our app state , it can also keep variables in sync with each other using reactive declarations.
 ```js
let count = 0;
$: doubled = count * 2;
```
- this is infact valid JS , which svelte means to re-run this code whenever any of the referenced values will change.
- so the state will change according to the value count in the event handler clicked.
- we could ofcourse just write {count * 2 } in the markup and not care about reactive values. But these become important when using state management in large values which are dependent on each other and not simple mutation.

### Statements:
- we are also not limited to declaring reactive values -> we can also run arbitary statements reactively. Eg: can log the value of count whenever it changes i.e in the $: < reactive-statement>.
- can group statements together in a block:
```js
$: {
console.log('the count is ' + count);
alert('I SAID THE COUNT IS ' + count);
}
```
- can even put $: in front of things like if blocks.
```svelte 
<!-- example of using multistate -->
<script>
	let count = 0;
	$: defaultState = "🐣🍼";
	$: logger = () => {
		if(count>18){
			alert('Legal Age to Drive!!! 🔥😈😭🫂');
			count = 0;
		} else {
			return defaultState;
		}
	}

	function handleClick() {
		count += 1;
	}
</script>

<button on:click={handleClick}>
	Clicked {count} {logger()}
	{count === 1 ? 'time' : 'times'}
</button>
```

### Updating Arrays and Objects:
- Svelte's reactivity is triggered by assignments.
- Methods that mutate arrays or objects will not trigger updates by themselves.
```svelte 
<script>
	let numbers = [1, 2, 3, 4];
	let numbers2 = [10,20,30,40];

	
	function addNumber() {
		numbers.push(numbers.length + 1);
		numbers = [...numbers,numbers.length +1];
	}

	function multiplyNumber(){
		numbers2.push(numbers2.length+1);
		numbers2 = [...numbers2,numbers2.length+1];
	}
	

	$: sum = numbers.reduce((t, n) => t + n, 0);
	$: product = numbers2.reduce((n1,n2) => n1*n2,1);
	</script>

<p>{numbers.join(' + ')} = {sum}</p>

<p>{numbers2.join(' * ')} = {product}</p>

<button on:click={addNumber}> Add a number </button>

<button on:click={multiplyNumber}> Multiply a number </button>
```
- Add a number will calls the addNumber fucntion, which will append a number to the array but wont trigger the recalculation of sum.
- To fix this we can assign it back to itself, using the spread syntax.
- Same rule applies to array methods like pop, shift and splice and to object methods like Map.set, Set.add etc.
- Assignment to properties of objects and arrays obj.foo += 1 , will work the same as assignments to the values themselves.
- Simple rule of thumb: Updated variable must directly appear on the left hand side of the assignment to trigger reactivity.

### Declaring Props:
- To pass data from one component down to its children, we need to declare properties, generally shortened to props.
- we do that using export keyword in svelte. this is not how export works in JS, but svelte compiler does some magic transformations.
- To pass the props we can use it like:
```svelte 
<Nested answer={42} question={"The age of universe"}/>
```
- where answer and question are props that are "exported".

#### Default Values in Props:
- we can easily specify default values for props in Nested.svelte
```js
	export let answer = "a mystery";
```
- If we now add a second component without an answer prop, it will fall back to the default.
#### Spread Props:
- If we have an object of properties, we can spread them into a component instead of specifying each one.
- **Rare Cases**: in case we need to reference all the props that were passed into a component, including ones that werent declared with export, we can do so by accessing \$$props directly. Hard for Svelte to optimize.
```svelte
<script>
	import Info from './Info.svelte';

	const pkg = {
		name: 'svelte',
		version: 3,
		speed: 'blazing',
		website: 'https://svelte.dev'
	};
</script>

<Info {...pkg} />
```



## Logic:
- HTML doesnt have a way of expressing logic, like conditionals and loops. Svelte does since its a compiler to JS.
- To conditionally render some markup, we wrap it up in a if block.
```svelte
<script>
	let user = { loggedIn: false };

	function toggle() {
		user.loggedIn = !user.loggedIn;
	}
</script>
{#if user.loggedIn}
<button on:click={toggle}> Log out </button>
{/if}
{#if !user.loggedIn}
<button on:click={toggle}> Log in </button>
{/if}
```
### else blocks
- since this condition is mutually exclusive , we can simplify the component slightly by using an else block:
```svelte 
<script>
	let user = { loggedIn: false };

	function toggle() {
		user.loggedIn = !user.loggedIn;
	}
</script>

{#if user.loggedIn}
	<button on:click={toggle}> Log out </button>
{:else}
	<button on:click={toggle}> Log in </button>
{/if}	
```
### else-if blocks
- multiple conditions can be 'chained' together with else if:
```svelte
<script>
	let x = 6;
</script>

{#if x > 10}
	<p>{x} is greater than 10</p>
{:else if x > 5 }
	<p>{x} is between 6 and 10</p>
{:else if x > 2}
	<p>{x} is between 3 and 5</p>
{:else}
	<p> {x} is between 0 and 2</p>
{/if}
```
### **each blocks**
- inc ase we need to loop over lists of data, we use an each block, can get the index as a second argument in each block.
```svelte
<script>
	let cats = [
		{ id: 'J---aiyznGQ', name: 'Keyboard Cat' },
		{ id: 'z_AbfPXTKms', name: 'Maru' },
		{ id: 'OUtn3pvWmpg', name: 'Henri The Existential Cat' }
	];
</script>

<h1>The Famous Cats of YouTube</h1>

<ul>
	{#each cats as cat,index}
	<li>
		Cat Index Number -> {index}&nbsp;
		<a target="_blank" href="https://www.youtube.com/watch?v={cat.id}" rel="noreferrer">
			{cat.name}
		</a>
	</li>
	{/each}
	<!-- close each block -->
</ul>
```
- can also use destructuring like in regular javascript -> each cat as {id,name} -> and replace cat.id and cat.name with id and name respectively.
### Keyed Each Blocks:
- By default when we modify the value of an each block , it will add and remove DOM nodes at the end of the block, and update any values that have been changed.That might not be what we might want.
- To make changes persistent with associated data, we specify an unique identifier("key") for each iteration of the each block.
- We can use any object as key, as Svelte uses a Map internally -> in other words we could do (thing) instead of (thing.id).
- Using a string or number is generally safer, however , since it means identity persists without referential equality, eg: for when updating with fresh data from an API server.
```svelte
<script>
	import Thing from './Thing.svelte';

	let things = [
		{ id: 1, name: 'apple' },
		{ id: 2, name: 'banana' },
		{ id: 3, name: 'carrot' },
		{ id: 4, name: 'doughnut' },
		{ id: 5, name: 'egg' }
	];

	function handleClick() {
		things = things.slice(1);
	}
</script>

<button on:click={handleClick}>
	Remove first thing
</button>

{#each things as thing}
	<Thing name={thing.name} />
{/each}
```
### Await Blocks:
- Use for dealing with asynchronous data . 
- We can directly await the value of promises directly in our markup.
```svelte 
{#await promise}
 <p>...Waiting</p>
{:then number}
<p> The number is {number}</p>
{:catch error}
<p style="color: orange">{error.message}</p>
{/await}
```
- Only the most recent promise is considered here, meaning we dont have to worry about race conditions.
- If we know that our promise can't reject, we can omit the catch block. We can also omit the first block if we dont want to show anything until the promise resolves:
```svelte 
{#await promise then number}
	<p>The number is {number}</p>
{/await}
```

## Events:
### DOM Events:
- we can listen to any DOM event on an element (such as click or pointermove) with the on: directive.
```svelte
<script>
	let m = { x: 0, y: 0 };

	function moveHandler(event) {
		m.x = event.clientX;
		m.y = event.clientY;
	}
</script>

<div on:pointermove={moveHandler}>
	The pointer is at ({m.x} x ,{m.y} y )
</div>

<style>
	div {
		position: fixed;
		left: 0;
		top: 0;
		width: 100%;
		height: 100%;
		padding: 1rem;
	}
</style>
```
### Inline Handlers:
- Event Handlers can also be defined inline , inside the component.
```svelte
<script>
	let m = { x: 0, y: 0 };

	function handleMove(event) {
		m.x = event.clientX;
		m.y = event.clientY;
	}
</script>

<div on:pointermove={(event) => {
	m = {x: event.clientX,y:event.clientY}
}}>
	The pointer is at ({m.x} x ,{m.y} y)
</div>

<style>
	div {
		position: fixed;
		left: 0;
		top: 0;
		width: 100%;
		height: 100%;
		padding: 1rem;
	}
</style>
```
- Compiler doesnt care if we do the in-line event handler or inside the script tag, both will be equally performant.

### Event Modifiers:
- DOM Event Handlers can have modifiers that will alter their behaviour.
- List of Modifiers:
	- preventDefault -> calls the event.preventDefault() before running the handler. Useful for client-side form handling.
	- stopPropogation -> calls event.stopPropogation(), preventing the event reaching the next element.
	- passive -> improves scrolling perf on touch/wheel events -> Svelte compiler will automatically add this when it is safe to do so.
	- nonpassive -> explicitly set passive: false 
	- capture -> fires the event handler during the capture phase instead of bubbling phase.
	- once -> removes the handler after the first time it runs.
	- self -> only triggers handler if event.target is the element itself.
	- trusted -> only will trigger the handler if event.isTrusted is true, meaning that the event was triggered by a user action rather than because some JS called element.dispatchEvent(...)
- Also chaining of modifiers are also possible.
```svelte
<button on:click|once={() => alert('clicked')}>
	Click me
</button>
```

### Components Triggering Events:
- Components can also dispatch events. To do so, they must create an event dispatcher.
```svelte 
<script>
	import Inner from './Inner.svelte';

	function handleMessage(event) {
		alert(event.detail.text);
	}
</script>

<Inner on:message={handleMessage}/>
```
```
<!-- inner.svelte -->
<script>
	import {createEventDispatcher} from 'svelte';

	const dispatch = createEventDispatcher();
	
	function sayHello() {
		dispatch('message', {
			text: 'Hello!'
		});
	}
</script>

<button on:click={sayHello}>
	Click to say hello
</button>

```

- createEventDispatcher() method must be called when the component is first instantiated -> can't do it later inside eg: a setTimeout callback. This will links dispatch to the component instance.
- And then we add a on:message handler in the App.svelte component.
- we can try to change the event name  and change the attribute name from on:message to on:greet.

### Event Forwarding:
- Unlike DOM events, component events don't [bubble](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Event_bubbling)
- if we want to listen to an event on some deeply nested component, the intermediate components must forward the event.
- In this case, all our component is "encapsulated" in the Outer componenet i.e only outer component being applied in App.svelte.
- we could solve the problem by adding a createEventDispatcher to Outer.svelte , listening for the message event and creating a handler for it.
- But that is a lot of code to write, so Svelte gives us an equivalent shorthand -> an on:message event directive without a value meaning that it needs to forward all message events.

### DOM Fetch Forwarding:
- Event Forwarding also works for DOM events.

## Bindings:
- As a general rule -> Svelte follows the same flow as React i.e it is top-down and unidirectional -> a parent component can set props on a child component , and a component can set attributes to an element, but not the other way round.