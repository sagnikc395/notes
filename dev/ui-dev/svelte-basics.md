---
title: Svelte Basics
tags:
  - frontend
  - svelte
date: 10/1/25
---
## What is Svelte ?
- Svelte is a tool for building web apps. Like other UI frameworks , it allows us to build our app declaratively out of components that combine markup, styles and behaviours.
- These components are compiled into small, efficient JS modules that eliminate overhead traditionally associated with UI frameworks.
- We can build our entire app with Svelte or we can add it incremently to an existing codebase. We can also ship components as standalone packages that will work anywhere 
```svelte 
<h1>Welcome!</h1>
```

## Introduction:
### First Component:
- In Svelte, an application is composed from one or more components. A component is a reusuable self-contained block of code that encapsulates HTML,CSS and JS that belongs together, written into .svelte fils. 
- To add JS to your file, add a script tag 
```svelte 
<script lang="ts">
	let name: string = "Svelte";
</script>

<h1>Hello {name} </h1>
```
- We can then refer to the variable in the markup inside the curly braces. Inside the curly braces , we can put any JS we want.
### Dynamic Attributes:
- Just like we can use curly braces to control text, we can use them to control element attributes.
```svelte 
<script>
	let src = '/tutorial/image.gif';
</script>

<img src={src} alt={"rick rolled"}/>
```

- We can use curly braces inside attributes.
- It's not uncommon to have an attribute where the name and value are the same, like src={src}. We can write it in shorthand as
```svelte 
<img {src} alt="{name} dances" />
```

### Styling
- Just like HTML, we can add a style tag to our component. 
- Importantly, these rules are scoped to the component. We won't accidently change the style of p elements elsewhere in our app.
```svelte 
<p> Some comment </p>

<style>
	p{
	color: orange;
	font-family: 'Comic Sans MS',cursive;
	font-size:1.2em; 
	}
</style>
```

### Nested Components:
- We can import components from other files and include them in our markup. 
- Adding a script tag to the top of our App.svelet that can import Nested.svelte.
```svelte 
%% App.svelte %%
<script lang="ts">
	import Nested from './Nested.svelte';
</script>
```
- and then we can include it in the main :
```svelte
<p> This is a paragraph </p>
<Nested />
```

- Even though the Nested.svelte has a `<p>` element , the styles from App.svelte don't leak in.

### HTML Tags:
- Strings ordinarily are inserted as plain text, meaning that characters like `<` and `>` have no special meaning.
- But sometimes we need to render HTML directly into a component. Eg: words that we re reading right now exists in a md file that gets included on the page as a blob of HTML.
- In Svelte, we do this with the special `{@html...}` tag.
```svelte 
<script>
	let string = `this string contains some <strong>HTML!!!</strong>`;
	let breakLine =`<br />`;
	let anotherString=`<h1>TopDawg !</h1>`;
</script>

<p>{@html string}</p>
<p>{@html breakLine}</p>
{@html anotherString}
```
- Imp: Svelte doesnt perform any sanitization of the expression inside before it gets inserted into the DOM. Need to manually check it otherwise we risk exposing our users to Cross-Site Scripting (XSS) attacks.

## Reactivity:

### State:
- At the heart of Svelte is a powerful system of reactivity for keping the DOM in sync with out application state - eg: in response to an event.
- Making the count declaration reactive by wrapping the value with `$state(...)`.
```svelte 
let count = $state(0);
```
- This is called as a rune, and it is how we tell Svelte that count isn't a ordinary variable. Runes look like functions, but they are not -> when we are using Svelte, they are the primitives of the language itself.
```svelte 
<script>
	let count = $state(0);
	let count2 = $state(-1);
	function increment() {
		// TODO implement
		count +=1;
	}
	function decrement() {
		if(count2===0){
			alert("Invalid!")
		}
		count2 -=1;
	}
</script>
<button onclick={increment}>
	Clicked {count}
	{count === 1 ? 'time' : 'times'}
</button>
<button onclick={decrement}>
	Clicked {count2}
	{count2 === 1 ? 'time' : 'times'}
</button>
```

### Deep State:
- State reacts to reassignments. But it will also reacts to mutations -> we call this as deep reactivity.
- Deep reactivity is implemented using proxies, and mutations to the proxy do not affect the original object.
```svelte 
%% making numbera reactive array  %%

<script>
let numbers = $state([1,2,3,4]);

//now we can change the array itself 
function mutateNumbersArray() {
numbers[numbers.length] = numbers.length + 1;
}

//we can also push to the array instead 
function addNumber(){
	let random = Math.floor(Math.random() * 10);
	numbers.push(numbers.length +1);
}
</script>
<p>{numbers.join(' + ')} = ...</p>

<button onclick={addNumber}>
	Add a number
</button>
```

### Derived State:
- often we need to derive the state from other state. For this, we have the `$derived` rune:
```svelte 
let numbers = $state([1,2,3,4]);
let numbers = $derived(numbers.reduce((t,n) => t+n,0));
```
- and then we can use this in our markup:
```svelte 
<p>{numbers.join(' + ')} = {total}</p>
```
- the expressions inside the `$dervied` declaration will be re-evaluated whenever its dependenices are updated. Unlike normal state, derived state is read-only.
```svelte 
<script>
	let numbers = $state([1, 2, 3, 4]);

	function addNumber() {
		let number = Math.floor(Math.random()*10);
		numbers.push(number);
	}
	let total = $derived(numbers.reduce((t,n) => t+n,0));
</script>

<p>{numbers.join(' + ')} = {total}</p>

<button onclick={addNumber}>
	Add a number
</button>
```
### Inspecting State:
- Often useful to be able to track the value of a piece of state as it changes over time.
- here numbers is a reactive [proxy](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy) There are a couple of things we can do.We can create a non-reactive snapshot of the state with `$state.snapshot(...)`.
```svelte 
function addNumber() {
	numbers.push(numbers.length+1);
	console.log($state.snapshot(numbers));
}
```
- We can use the `$inspect` rune to automatically log a snapshot of the state whenever it changes. This code will automatically be stripped out of our production build.
```svelte 
function addNumber() {
	numbers.push(numbers.length+1);
}
$inspect(numbers);
```

- We can customize how the info is displayed by using `$inspect(...).with(fn)` -> can use `console.trace` to see where the state change originates from 
```svelte 
$inspect(numbers).with(console.trace);
```

```svelte 
<script>
	let numbers = $state([1,2,3,4]);
	let total = $derived(numbers.reduce((t,n) => t+n,0);

	function addNumbers() {
		numbers.push(numbers.length+1);	
	}
	$inspect(numbers).with(console.trace);
</script>
<p>
{numbers.join(' + ') = {total}}
</p>

<button onclick={addNumber}>Add a number</button>

```

### Effects:
- State is only reactive if something is reacting to it, else it is just a sparkling variable.
- Effect -> ones that Svelte creates on our behalf to update the dom in response to state changes -> but we can also create our own with the `$effect` rune.
```svelte 
<script lang="ts">
	let elapsed = $state(0);
	let interval = $state(1000);

	$effect(() => {
	setInterval(() => {
	elapsed += 1;},
	interval);
	});
</script>
```
- We are not clearing out the old intervals,when the effect updates. We can fix that by returning a cleanup function:
```svelte 
$effect(() => {
const id = setInterval(() => {
	elapsed += 1;
}, interval);

return () => {
	clearInterval(id);
};
})
```
- Cleanup function called immediately before the effect function re-runs when interval changes, and also when the component is destroyed. 
- If the effect function doesn't read any state when it runs, it will only run once, when the component mounts.
- Note: Effects do not run during server-side rendering.
### Universal Reactivity:
- We can use runes outside components, for example: to share some global state.
- `<Counter />` components in this exercise are all importing the counter object from shared.js. But it's a normal object, and as such nothing happend when we click the buttons. We can wrap the object in `$state(...)`
```js 
export const counter = $state({
count: 0,
});
```
- But this will cause errors, as we can't use runes in normal .js files, only .svelte.js files. We rename the file to shared.svelte.js.
- We can then update the import declaration in `Counter.svelte`:
```svelte 
<!-- Counter.svelte -->
<script lang="ts">
	import { counter} from './shared.svelte.js';
</script>
```
- Note: we cannot export a $state declaration from a module if the declaration is reassigned (rather than jus mutated), because the importers then would have no way to know about it.

## Props:

### Declaring Props:
- Till now, we have only dealt exclusively with internal state -> the values are only accessible withing a given component.
- In any real applications, we will need to pass data from one component down to its children. To do that, we need to declare properties, or props. In Svelte we do that using `$props` rune.
```svelte 
<script lang="ts">
	let {answer} = $props();
</script>
```

```svelte 
<script>
	let { answer } = $props();
	let currState = $state(answer);
	$inspect(currState).with(console.trace);
</script>

<p>The answer is {answer}</p>
```

### Default Values:
- We can easily specify default values for props in `Nested.svelte`
```svelte 
<script lang="ts">
	let {answer = 'a mystery'} = $props(); 
</script>
```
- Now if we add a second component without an answer prop, it will fall back to the default:
```svelte 
<script>
	import Nested from './Nested.svelte';
</script>

<Nested answer={42}/>
<Nested />
```

### Spread Props:
- In `App.svelte` we have forgotten to pass the `name` prop expected by `PackageInfo.svelte` meaning the `<code>` element is empty and the npm link is broken.
- We can fix it by explicitly adding the prop.
- But since the properties of `pkg` correspond to the component's expected props, we can 'spread' them onto the component instead.
```svelte 
<PackageInfo {...pkg} />
```

- In the PackgeInfo.svelte we can get an object containing all the props that were passed into a component using a rest property:
```svelte 
let {name, ...stuff} = $props();
```
- Or by skipping destructuring altogether:
```svelte 
let stuff = $props();
```
- where we can access the properties by their object paths:
```svelte 
console.log(stuff.name,stuff.version,stuff.description, stuff.wesbite);
```

### if blocks:
- HTML doesnt have a way of expressing logic, like conditionals and loops. Svelte does.
- To conditionally render some blocks, we wrap it in a `if ` block. 
```svelte 
<button onclick={increment}>
	Clicked {count}
	{count === 1 ? 'time' : 'times'}
</button>

{#if count > 10}
	<p>{count} is greater than 10</p>
{/if}
```

### else blocks:
- Just like JS , an if block can have an else block:
```svelte 
{#if count > 10}
	<p>{count} is greater than 10</p>
{:else}
	<p>{count} is betwen 0 and 10 </p>
{/if}
```
- `{#...` opens a block. `{/...}` closes a block. `{:....}` continues a block. 

### else-if blocks:
- Multiple conditions can be 'chained' together with `else if`
```svelte 
{#if count > 10}
	<p>{count} is greater than 10</p>
{:else if count < 5}
	<p>{count} is less than 5 </p>
{:else}
	<p>{count} is between 5 and 10</p>
{/if}
```

### each blocks:
- When building UI we will often find ourself working with lists of data.Instead of labourisuly copying, pasting and editing, we can get rid of all but the first button, then use an `each` block:
```svelte 
<div>
	{#each colors as color}
		<button
		style="background: red"
		aria-label="red"
		aria-current={selected === 'red'}
		onclick={() => selected = 'red'}
		></button>
	{/each}
</div>
```
- here colors can be any iterable or array-like objects - in other terms , anything that works with `Array.from`.
- We can get the current index as a second argument:
```svelte 
<div>
	{#each colors as color,i}
		<button
			style="background: {color}"
			aria-label={color}
			aria-current={selected === color}
			onclick={() => selected = color}
		></button>
	{/each}
</div>
```
```svelte
<script>
	const colors = ['red', 'orange', 'yellow', 'green', 'blue', 'indigo', 'violet'];
	let selected = $state(colors[0]);
</script>

<h1 style="color: {selected}">Pick a colour</h1>

<div>
	{#each colors as color}
	<button
		style="background: {color}"
		aria-label="{color}"
		aria-current={selected === color}
		onclick={() => selected = color}
	></button>
{/each}
</div>

<style>
	h1 {
		font-size: 2rem;
		font-weight: 700;
		transition: color 0.2s;
	}

	div {
		display: grid;
		grid-template-columns: repeat(7, 1fr);
		grid-gap: 5px;
		max-width: 400px;
	}

	button {
		aspect-ratio: 1;
		border-radius: 50%;
		background: var(--color, #fff);
		transform: translate(-2px,-2px);
		filter: drop-shadow(2px 2px 3px rgba(0,0,0,0.2));
		transition: all 0.1s;
		color: black;
		font-weight: 700;
		font-size: 2rem;
	}

	button[aria-current="true"] {
		transform: none;
		filter: none;
		box-shadow: inset 3px 3px 4px rgba(0,0,0,0.2);
	}
</style>

```

### keyed-each-blocks:
- By default, when we modify the value of an each block, it will add and remove DOM nodes at the end of the block, and update any values that have changed. That might not be what we want.
- Svelte works different than React -> the component 'runs' once, and then subsequent updates are 'fine-grained'. This makes things faster and gives us more control.
- One way to fix it would be to make `emoji` a `$derived` value. But it makes more sense to remove the first `<Thing />` component altogether rather than remove the last one and update all the others.
- For this, we specify a unique key for each iteration of the each block.
```svelte 
{#each things as thing (thing.id)}
	<Thing name={thing.name} />
{/each}
```

- We can use any object as the key -> Svelte uses a Map internally -> in other words we can to `(thing)` instead of `(thing.id)`. Using a string or number is generally safer, however it means identity persists without referential equality, for eg: when updating with fresh data from an API server.
```svelte 
<!-- Thing.svelte -->
<script>
	const emojis = {
		apple: '🍎',
		banana: '🍌',
		carrot: '🥕',
		doughnut: '🍩',
		egg: '🥚'
	};

	// `name` is updated whenever the prop value changes...
	let { name } = $props();

	// ...but `emoji` is fixed upon initialisation
	const emoji = emojis[name];
</script>

<p>{emoji} = {name}</p>
```
```svelte 
<!-- app.svelte -->
<script>
	import Thing from './Thing.svelte';

	let things = $state([
		{ id: 1, name: 'apple' },
		{ id: 2, name: 'banana' },
		{ id: 3, name: 'carrot' },
		{ id: 4, name: 'doughnut' },
		{ id: 5, name: 'egg' }
	]);
</script>

<button onclick={() => things.shift()}>
	Remove first thing
</button>
<button onclick={() => things.pop()}>
	Remove Last Thing
</button>

{#each things as thing}
	<Thing name={thing.name} />
{/each}

```


### await blocks:
- Most web apps have to deal with async data at some point. Svelte makes it easy to await the value of a promise directly in our markup.
- Also the most recent promise is considered, meaning we don't need to worry about race conditions.
```svelte 
{#await promise}
	<p>...rolling</p>
{:then number}
	<p>You rolled a {number}</p>
{:catch error}
<p style="color:red">{error.message}</p>
{/await}
```
- If we know that the promise can't reject, we can omit the catch block. We can also omit the first block if we don't want to show anything until the promise resolves.
```svelte 
{#await promise then number}
	<p>You have rolled a {number}!</p>
{/await}
```
```js
//utils.js
export async function roll() {
	// Fetch a random number from 1 to 6
	// (with a delay, so that we can see it)
	return new Promise((fulfil, reject) => {
		setTimeout(() => {
			// simulate a flaky network
			if (Math.random() < 0.3) {
				reject(new Error('Request failed'));
				return;
			}

			fulfil(Math.ceil(Math.random() * 6));
		}, 1000);
	});
}

```
```svelte 
<!-- app.svelte -->
<script>
	import { roll } from './utils.js';

	let promise = $state(roll());
</script>

<button onclick={() => promise = roll()}>
	roll the dice
</button>

<!-- promise stores the value of the promise on button click-->
{#await promise}
<p>...rolling</p>
{:then result}
	<p>You have rolled a {result}!</p>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}
```

### DOM events:
- 