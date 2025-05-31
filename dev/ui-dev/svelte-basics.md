---
title: Svelte Basics
tags:
  - frontend
  - svelte
  - ui
date: 31/5/25
---
## Introduction to Svelte and Signal Based Reactivity

### What is Svelte ?

- Svelte provides a way to build declarative ,state driven user interfaces.
- It uses a compiler to turn declarative components in HTML,CSS and JS into lean,tightly optimized JS.
- Reduces overhead and makes the build size small.
- Svelte has a powerful system of reactivity for keeping the DOM in sync with our application state using a set of symbols called Runes.
- Runes are symbols that we use in Svelte files to declare state, derived values, side effects and more.
- They can not only be used inside of components but also in normal JS modules -> allowing for universal reactivity.
- Derived values are going to run sycnhronously, while effects are going to be synchronized in the microtask queue.
- Dependency graph of our states and values:

![alt text](image.png)


- Dont use effect to sync states, rather use effects to sync side effects.
- Svelte uses signal based reactivity to sync changes and whatever we use it it will create a side effect on where our changes will be reflected.
- In Svelte when we update the state, it runs immediately and it can run the state as soon as possible, while in React the virtual DOM will take control and delay the response.
- In Svelte, the script tag will run only once, so dervied things need to be present in special syntax($derived) -> and recalculated whenever count updates. (updated value on someone else)
- To create side effects we use the effect rune ($effect) and we do not need to use effect rune to get the latest value.
### Svelte vs Svelekit

#### Svelte
- Component based JS framework.
- Allows us to build state driven components for the web in a declarative way.
#### SvelteKit
- Sveltekit is a framework for building extremely high performance web apps.
- Routing, perfetching, offline support ,SSR , progressive enhancement and more.
- Sveltekit to Svelte is like Nextjs to reacjs or nuxtjs to vue.