## React Foundations

- Understanding React from foundations.
- Jargon we will understand:

  - JSX
  - class vs className
  - static vs dynamic websites.
  - state
  - components
  - re-rendering

- a lot of mathamticaticla things and object lifecycle things that we have to write for large applications we have to write in DOM.

- React came into the picture. React is a easier syntax to write normal HTML/CSS/JS. It under the hood gets converted to HTML/CSS/JS.
  React is just one syntax that gets converted into JS files only, but we as a developer write code as React.

### Why React ?

- People realized that its harder to do DOM Manipulation the conventional way.
- There were libraries that came into the picture that made it slightly easy, but still for a very long app its way harder(jquery).
- Eventually, Vuejs/React created a new syntax for the frontends.
- Under the hood, the React compiler converts our code to HTML/CSS/JS.

### State, Components and Re-rendering:

- State is an object that represents the current state of the app.
- It represents the dynamic things in our app -> things that change.
- Eg: the value of the counter.

- Components :- how a DOM element should render , given a state. It is a reususage , dynamic component how should it render.

- when we write a React application for the topbar , we have the state and a bunch of components defined -> it is a HTML snippet that is present and we put the items there.

- Give me a state of the application -> the dynamic nature of the application , give me the individual components and how they are connected together , React will take care of updation logic.

- Re-rendering -> if we update the state -> the no of notifications have gone up; and the developer changes the state and React does the re-rendering behind the hoods.
- A state change triggers a re-render. A re-render represents the actual DOM being manipulated when the state changes.
- React does the virtual DOM -> representation of the current state in memory to calculate the difference of the current state to the previous one.

- We usually have to define all our components once, and then all we have to do is update the state of our app, React will take care of re-rendering our app.
  
### JSX 
- JS file into which we can write both html and XML.
- Both the state and the styling can be written in the same file.
- App.jsx, main.jsx -> npm run build -> builds a dist/ folder having a index.html and index.js file that is served to the client and can host in AWS as a fully functioning app.

### Pause:
- We have learnt till now:
  - How to create an empty react app
  - index.html, main.jsx -> App.jsx 
  - build into dist folder

### Writing a Dynamic Website 
- State + Components
- Given an state and a component and a logic to render them, React re-renders on its own.
- React will automatically know that this has been increased, so it will change accordingly.
- React does not look at every variable as a state variable, React says that if you want your variable to be a state variable, you have to do a certain way so that it is watching it.
- useState (a hook) is required to update them, we simply cannot use our own global variables to update them.
- so useState returns 2 things, the state itself and the updation logic that will update it -> the React will under the hood implement the onButtonPress under the hood.
- As we update our state variables, the application changes according to that.
- 