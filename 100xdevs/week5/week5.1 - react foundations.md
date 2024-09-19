---
title: React Foundations
tags:
  - react
  - user-interface
---
- React Foundations notes.
- Shallow dive / Overview of React Concepts.
- Want to understand why React was Introduced ,some jargons like:
	- jsx 
	- class vs className 
	- static vs dynamic websites
	- state 
	- components 
	- re-rendering 
- Static websites -> that doesnt change its content , once its content is loaded. Things that is rendered -> pretty much is static -> whose HTML is changing as time goes by -> not the biggest use case for React.

- For dynamic websites, React makes it easier to do dynamic manipulation i.e contents of page due to user triggered events.
- Sort of hard of write , the Javascript part define the part on button press, gets the dom element internal value.
- React eventually gets converted to HTML/CSS and JS.
- Why React ?
	- People realized that its harder to do DOM manipulation the conventional way.
	- There were libraries that came into the picture that made it slightly easy, but still for a very big app it's way harder(JQuery)
	- Eventually React/ VueJS created a new syntax to do frontends.
	- Under the hood, the react compiler converts our code into HTML/CSS/JS.

- React Jargon :
	- 2 create a React App , need to think about 3 things:
		- Components 
		- State 
		- Re-rendering 
	- Components and State are standard things that we have to write , everything else React takes care of.
	- State -> An JS object that represents the current state of the app. It represents the dynamic things in your app (things that will change). Eg: the value of the counter.
		 Eg: ```js 
			 {
			 count :1 }```
			Eg: For the top bar of linkedin:
			```js 
			{
			topbar: {
			base: 0 ,
			jobs:8,
			notifications: 25,
			}
			}```   
	- Components -> How a DOM element should render, given a state. It is a reusuable, dynamic,HTML snippet/chunk that changes, given the state.
	- and how the state is connected to this component.
	- React takes care of updating this changes under the hood.
	- Re-rendering -> user updating the state in the component , it takes the current input, and puts on it on the DOM.
		- A state changes triggers a re-render.
		- A re-render represents the actual DOM being manipulated when the state changes.
		- Virtual DOM is the current DOM that React keeps in memory and uses it to keep the difference between the previous DOM and the current DOM.
	- We usually have to define all of our components once, and then all we have to do is update the state of our app , React will take care of the re-rendering of our app.
	- React uses the components that we have defined, using the state and getting back the button component that we have got and getting it back, putting it back from the DOM -> i.e re-rendering the DOM and put the values on the DOM.
		- First clear the DOM and then put the new item on the DOM.
	- Code Flow:
		- (in ref to dom-counter.js)
		- an empty div gets created.
		- an empty state gets defined.
		- bunch of function defintions.
		- then the re-render function call is triggered.
		- The state is what your application should look like.

### Creating a React Project 
- npm create vite@latest -> using vite as a bundler and followed by name of the project.
- JSX files -> Async JS with HTML string literals.
- main.jsx -> take the root defined in the index.html and inject the js file into it.
	1. Create an empty React App
	2. index.html , main.jsx -> app.jsx -> hi there
	3. dist -> index.html -> js syntax
- whenever we have to wrap a dynamic varibale inside a component, wrap inside {} quotes.
- JSX -> Javascript + XML -> 
```jsx 
	function onClickHandler() {
		alert("hi there");
	}
```
- even though we update the state as :
```jsx
  

function onClickHandler() {

state.count = state.count + 1;

console.log(state.count);

}
```
- the reason it is not updating is that React does not look at every variable as a state variable that will make change.
- React requires we define the state variable in such a way that we are watching it, if we are not watching it for changes, it cannot update the DOM.

### useState:
- a hook that is used to define the state.
- it returns a state and a update function to update it.