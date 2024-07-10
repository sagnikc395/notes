---
title: recoil and state management
tags:
  - recoil
  - state-management
  - atoms
---


- for managing the state of the applications
- from normal react to how state management is managed in react.
- recoil -> state management tool 
	- why is required ?
	- inside our component we are defining the items
- AppBar ->
	- has a username and asetuseremail -> for setting up the component for the first time and the init function is called.
	- moving away from using callbacks to using axios and async functions.
	- The AppBar need to render signup/signin button or add user and logout button.
	- the thing to be rendered is dependent of the login status.
	- once the state variable is set , we conditonally render the given item.
- Introducing state management tools and recoil:
	- why state management is required and how does it work ?
		- Right now we define state varibales inside components and free filling it however we want.
		- Problems:
			- User State is accessible in the Appbar component and if we look up in the landing page.
- Wrap the whole of the app state in the recoil root and paste it.
- react doesnt know it needs to re-render and pull the thing from localStorage and needs to constantly update it
- 