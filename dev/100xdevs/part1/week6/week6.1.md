## React Hooks

- React Deeper Dive
- what react returns, re-rendering, keys, wrapper components
- useEffect, useMemo, useCallback, useRef.

### React component returns:

- A component can only return a single top-level xml.
- Why ?
  - Makes it easy to do reconciliation.
  - the process of figuring out what DOM updates need to happen, as our application grows.

### re-render

- anytime React actually does the DOM Manipulation and puts on the DOM , is called the React Re-render.
- React creates dynamic websites

  - the content of what changes quickly.
  - anytime such dynamic features happen, is called as a re-render.

- Whenever the DOM updates happen, it re-renders the DOM to make the new changes.
- The room of improvement in React is to minimize re-renders.
  - Eg: making a mobile app in react native or real-time game written which shows actual lagging , need to improve the re-rendering in that.
- **We are only re-rendering the things that need to be re-rendering and the static things should remain the same**.(i.e makes a diff of changes that are required and apply those changes.)

- A re-render means that :

  - React did some work to calculate what all should update in this component.
  - The component actually got called(we can put a log to confirm this)
  - The inspector shows us a bouding box around the component.
  - i.e this function was called by React.

- It will happen when:

  - A state variable that is being used inside a component changes.
  - A parent component re-render triggers all the children re-rendering.
  - If it title is present in the lifecycle of it and setTitle is ever called, it would re-render and if any parent re-renders then all children will trigger a re-render for all children.

- **Objective**: You want to minimize the number of re-renders to make a highly optimal react app , the more the components that are gettin re-rendered , the worse.

- Push the state down:
  - if we know the state variable used in the header only, why not push it down to the header.
  - until we react state management , the state propogation only occurs top-down;
  - rule of thumb: multiple children/multiple components, we need to find their lowest common ancestor and we store it there / or we can push it down as much as we can.
- React.Memo (i.e memoization):

  - memo lets us skip re-rendering a component when its props are unchanged.
  - whenever you want to memoizing a component you want to memoize -> i.e not change it we can do like

  ```js
  const Header = React.memo(({title}) {

  })
  ```

  - the parent re-renders (in our example of header), but the individual children don't(which doesnt have any state changes).

### keys in react :

- Creating a simple todo app that renders 3 times:

  - create a todo component that accepts title, description as input
  - initialize a state array that has 3 todos
  - iterate over the array to render all the TODOs
  - a button in the top level App component to add a new TODO.

- each child in a list need to have a unqiue key prop. Whenever the re-render happens, React can optimize the render the things by comparing the keys and can be used as a unique identifier.

### wrapper components:

- we can create a wrapper card component that takes the inner React component as an input.
- we can encapsualte components under each other and return a single parent component outside.

### useMemo,useCallback , useEffect:

- hooks in react are functions that allow us to "hook into" React state and lifecycle features from the function components.

- these functions that start with use are called as hooks.

- hooks in react are:

  - useEffect
  - useMemo
  - useCallback
  - useRef
  - useState
  - useReducer
  - useContenxt
  - useLayoutEffect

- lifecycle methods:

  - mounted -> first time when it gets rendered.
  - whenever component mounted/ unomunts i.e from the DOM, or renders the control would reach over to that function.

- these components allow us to make state changes and maintain a lifecycle event -> i.e when the component mounts, do something according to the hook.

- Exercise to get it better:

  - create an app that polls the sum server and gets the current set of TODOs and renders it on the screen.

-
