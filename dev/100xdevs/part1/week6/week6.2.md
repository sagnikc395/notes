## useCallback, useMemo and useEffect

- common hooks in react:

  - useEffect
  - useCallback
  - useMemo
  - custom hooks
  - prop drilling

- Two jargons we should know:

  - side effects:
    - in React, the concept of side effect encompasses any operations that reach outside the functional scope of a React component. These operations can affect other components, interact with the browser or perform async data fetching.
    - anything not related to renddering -> like fetching data from backend , directly manipulating the dom etc. are called as side effects as they are not part of the main react rendering cycle.
    - this async call, to fetch data from backend , can be classifed as a side effect => because these need to be seperate from our rendering cycle.
    - they shouldn't necessarily collude with the rendering cycle.
  - hooks:
    - hooks are a feature introduces in React 16 that allows us to use state other react featurees without writing a class.
    - they enable functional components to have access to stateful logic and lifecycle features, which were previously only possible in class components. This has led to a more concise and readable way of writing components in React.

### useState:

- lets us describe the state of our app. whenever state updates, it triggers a re-render which will finally results in a DOM update.

### useEffect:

- allows us to perform side effects in functional components -> settimeout, set internal etc.
- side effects are operations that can affect other components or can't be done during rendering like data fetching, subscriptions or manually changing the DOM in React components.
- useEffect hook serves the same purpose as componentdIDmOUNT , componentDidUpdate, componentWillUnmount in React class components, but unified into a single API.
- useEffect will only run the first load we are running, when no state parameters were provided to the component.
- if the component has a state variable, then we it will change according to the state variable.
- if we pass the id as a parameter to the dependency array in useEffect, it will track those changes and update those state variables only like for example when a state change occurs.

### useMemo:

- let's first understand what even is memo.
- memoization:
  - mildy DSA concept
  - it means remembering some ouput given an input and not recompute it again.
  - like caching
- eg: lets say in a f1 race you are a race driver and you wnat to check how much petrol is left. Would you do that in every lap?
- Similary, if we need to build an app that does 2 things:
  - increases a counter by 1 .
  - lets user put a value in an input box(n) and we need to show sum from 1-n.
  - restriction : eveything needs to inside the App.
- in our app example, we are using useState again and again and re-renders are happening for each value again -> we don't need to remmeber this expensive opeartion -> rather we should remember the value -> across the app.
- derivative events , or some thing that is computed and result is based on that we use useMemo for that, useEffect is for other lifecycle events.
- anything we do with useMemo we can use with useEffect.

### useCallback:

- used to memoize functons, which can help in optimizing the performance of our application, especially in cases involving child components that rely on reference equality to prevent unnecessary renders.(unless any dependency changes, until then return the function itself.)
- reference equality meaning pointing to the same location in memory.
- equal by value is different from equal by reference.
- **difference bw useMemo and useCallback**:
  - useMemo returns and stores the calculated value of a function in a variable.
  - useCallback returns and stores the actual function itself in a variable.

- for useMemo put the expensive operation in useMemo block so as to not re-render eveery time rather render once only.

- useEffect for async effects, useMemo for sync effects.
- anything other than functions, we can memoize using useMemo, for functions we memoize using useCallback.

## Custom Hooks:

- we can define our own hooks to encapsulate our own functions.
- only condition is - it should start with use (naming convention).
-

#### 