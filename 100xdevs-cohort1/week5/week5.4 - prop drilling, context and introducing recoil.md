---
title: prop drilling, context and introducing recoil
tags:
  - prop-drilling
  - contexts
  - recoil
---
- state change varibale count is being used by 2 different items 
- they are sharing the state and when the button is pressed is the only thing that needs DOM manipulation and that will update.
- Prop Drilling:
	- when we send down prop from top to bottom, the child may/may not require the items from the props.
	- better to send only the thing that are required from the parent to the child components.
	- ugly to keep sending the props the chain ,when only the first and the last guy needs it.
	- to prevent this we use the context api.
	- define a global level CountContext using createContext and wrap the whole app using the CountCOntext.Provider :
		- as this is providing those varibales as some point on the change.
		- and give them a value -> a string/ object 
			- object passing here -> count variable 
			- and a setCount value to it 
- using this we dont need to pass the props individually in this where they are require, they are passed magically and also not requires as props , and also as function arguments.
- using contexts there no longer prop drilling is not happening,but not prevents extra renders.
### prevent extra renders:
- state management libraries like zustand and recoil introduced to reduce the number of re-renders and to optimize the builds.
- replace the contextApi with Recoil.
- define the context outside of the root tree in the bottom of the file
- define a state using atom:
```js
const countState = atom({

key: "countstate", //unqiue id

default: 0, //default value for this thing

});
```
- and then add to our component,where we know the state will be re-rendered:
```jsx 
const CountComponent = () => {
//whenever
const count = useRecoilValue(countState);
return (
<div>
<Typography variant="h5" textAlign={"center"}>
{count}
</Typography>
</div>
);
};
```
- recoil will only change the thing only when the state will change and will be the same with the useRecoil value.