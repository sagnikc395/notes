---
title: SvelteKit Notes
tags:
  - svelte
  - ui
  - frontend
date: 12/4/25
---
### Pure Functions 

- A function that always returns the same output given a specific input and does not produce any side effects.
- Memoization :
	- Caching function results given a certain input to avoid rerunning the function again.

### Microtask Queue
```js 
function lo2() {

}

setTimeout(() => {
console.log("3");
},0);

log2();

Promise.resolve().then(() => {
console.log("4");
});

console.log("5");
```