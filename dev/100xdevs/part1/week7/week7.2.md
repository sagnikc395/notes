## Context, State Management and Recoil

- In the Context api, we can define the state variables slightly outside the component tree. and whatever components wants to use count, they can directly use it and we dont have to drill it.
- helpful for distant children of passing down the props and makes it slightly prettier.

### Downsides of using Context that require the internvation of state mangement tools:

- we might intuitively expect that , c2 should not re-render and never uses the count variable and the state variable only used by c1 and c4, so re-render should only be used by them.
- but that is not the case.
- need a tool/ method that can handle the problem of who is not using the state variable shouldnt re-render.
- state management libraries let us do that.

-**Why do you use the Context API? To make rendering more performant?** - no , it does not. - rather to make syntax cleaner/ get rid of the the prop drilling. - Doesnt fix re-rendering, only fixed prop drilling.

- solution that provides both good rendering and make the syntax more cleaner -> state management library.

### State Management using Recoil.

- A cleaner way to store the state of your app. Until now , the cleanest thing we can do is to use the Context API. It lets us teleport the state.
- But there are better solutions that get rid of the problems that Context API has (unncessary re-renders).

### Recoil:

- A state management library for React written by some ex React folks.
- Other popular ones:

  - Zustand
  - Redux.(not used in new projects)

- Recoil has the concept of atom to store the state i.e the smallest information of state. Rather than using useState, atom is the smallest information.
- An atom can be defined outside the component, or it can be teleported to any component.
- atom -> useState -> atom is the state variable in the recoil variable. get, update method.
- using atoms, we can define the component tree however we want, not necessarily a tree, and the atom will always be defined outside.
- any good open source project using state management solution, uses store to store their logic in a seperate file and don't use prop drilling or context api.

#### Things to learn in Recoil:

- RecoilRoot
- atom
- useRecoilState
- useRecoilValue
- useSetRecoilState
- selector

- create a seperate store/atoms folder to store the atoms. -> store all of our atoms here.

- useRecoilState, useRecoilValue , useSetRecoilState are the 3 apis we will be using extensively to interact with the state management.

- kinda look hooks in recoil.
- useRecoilState -> useState , 1:1 mapping of count and setCount
- useRecoilValue -> gives us just the value.
- useSetRecoilValue -> only we want to update variable and not want to access it.

- we choose the right hook and get the item for it.

- RecoilRoot component ->

  - like context api, we have to encapsualte the App component under the Context.Provider under the state logic, similarily here we have to wrap under the RecoilRoot to manage the state.

- selector:

  - lets say we need to render it is even , if the given count is even.
  - selectors represents a piece of dervied state. We can think of this as derviced state as the output of passing state to a pure function that dervices a new value from the old state.

-
