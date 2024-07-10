---
title : state management in react 
tags: hooks, effects,state-management, react, frontend
---

- biggest peak thoroughout the course; learning react is difficult and the best part is to learning on the go and making a lot of websites and is a better way to learn and things.
- don't directly jump into theoretical stuff , learn hands on and then go into the theory part.
- To learn:
	- Array Rnedering(maps,filters)
	- renders(setInterval example)
	- hooks (useState,useEffect)
	- TODO App
	- Custom Hooks

### Components:
- rendering arrays 
- maps and filters

- the file inside the root file is the final client side javascript that is being shipped.


### hooks 
- useState are what is called as a hook in react.
- hook was something that was named by the react folks.
- sort of a thing that remains independent of re-renders.
- counter remained the same even though the re-render happens.
- Math.random() only get called the first time the hook state got called.
-  hooks across re-renders protects the variables.
- the job of the useState is to initialise the value to the first item and then watching the diff , update according to the second parameter.
- another hook -> useEffect.
- take a single function as input and a array -> used to render only once, for subsequent re-rendering this gets guarded and does not run again.
- now using useEffect we can put our setInterval code inside this and call this multiple times and prevent it from infintily rendering.


- can also abstract away our hook , to make it custom.
- to make our hook instant, we can pass a time period to make it check automatically and autoupdate.