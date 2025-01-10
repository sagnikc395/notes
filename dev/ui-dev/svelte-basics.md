---
title: Svelte Basics
tags:
  - frontend
  - svelte
date: 10/1/25
---
### What is Svelte ?
- Svelte is a tool for building web apps. Like other UI frameworks , it allows us to build our app declaratively out of components that combine markup, styles and behaviours.
- These components are compiled into small, efficient JS modules that eliminate overhead traditionally associated with UI frameworks.
- We can build our entire app with Svelte or we can add it incremently to an existing codebase. We can also ship components as standalone packages that will work anywhere 
```svelte 
<h1>Welcome!</h1>
```

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
- 