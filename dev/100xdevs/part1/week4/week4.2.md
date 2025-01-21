## React Foundations :

- Implement a part of the React reconciler , creating solid foundations of React and why it was written a certain way.

- Jargon: DOM Manipulation:

  - Linkedin is heavily dynamic -> HTML we got back from the server is updated heavily.
  - React makes is slightly easier and help in developing them easily.
  - Append them one by one, slowly and slowly.
  - HTML being injected into the DOM via JS.
  - DOM Manipulation is very hard to write as a developer, making dynamic websites, with the websites that the DOM provides us a developer.

- Creating a TODO application with the TODO title and description and a button to add todo. It renders a TODO list and then a button to mark it as done.

- we are appending elements one by one, using innerHTML would completely overwrite that and that's not what we want.
- we need to do something extra, something jarring.
- need to use document.createElement, document.appendChild to append items to our DOM Tree.

### DOM Manipulation Downsides:`

- Very hard to add and remove elements.
- No central state management.
- Replication of state handling:
- what if there is a sevrer where these todos are put ?
- what if you update a TODO from our moile app, will you get the new array of TODOs on the frontend, how will you update the DOM then ?
- Only have addTodo function, also dont have an updateTodo or removeTodo function yet.

### In real websites, they will not tell us what to add or remove from our DOM, rather we need to compute the state of our DOMs.

- If we can write a function, that takes the state as an input and creates the output on the right, that is much more powerful that our original approach.

- we have a dynamic frontend that we want to do with a single function call, we wont need to destruct,create etc again and again on our own, rather we create helper function, create a window.setInterval , every 5 sec,set a request to the sum server and send a request and get the request.

- React effectively asks for a state and a few other things, and makes the state changes on its own and we dont have to care about the low level lifecycle methods.

- In real world, we can define any application and define them as a state in the application.

### Better Approach:

- In our crude approach, we are changing and re-rendering the whole DOM upfront.
- This is a expensive approach, rather update it based on what has changed.
- Question is, how does it calculate all that has changed ?
- Has a todo been marked as complete ?
- Has a todo been removed from the backend ?
- Better way to do is if there is a changed, you calculate the diff, then update the specific element in the DOM and based on the diff, update the DOM.(dont' re-render the whole DOM). -> Slighly a better way to solve the old problem.
- remember the old todos in a variables -> the old state -> **place where they have a blueprint of the DOM**

### Dynamic Frontends:

- So basically a dynmaic frontend does these these things:

  - Update a state variable
  - Delegate the task of figuring out the diff to a hefty function.
  - Tell the hefty function how to add, update and remove the elements.

### Structure of React:

- src/main.jsx file:
  - entry point to the react
  - imports react,reactdom for the website, dom for web base rendering.
  - ReactDOM.createRoot -> create a app tag and starts a entry point into the folder.
- src/app.jsx ->
  - render a HTML from a JS like syntax -> can return some HTML from the JSX codeblock.
  -

### Virtual DOM:

Virtual DOM
The concept of a Virtual DOM comes into play when dealing with efficient updates to the actual DOM.
The Virtual DOM is a lightweight copy of the actual DOM. When updates are made to the state of an application, a new Virtual DOM is created with the changes. This Virtual DOM is then compared with the previous Virtual DOM to identify the differences (known as "diffing").

In the context of a todo application:
State Changes:
If a todo has been marked as complete or removed from the backend, the state of the application changes.
Virtual DOM Comparison:
The new state is used to create a new Virtual DOM.
This new Virtual DOM is compared with the previous Virtual DOM.
Identifying Changes:
The difference between the new and previous Virtual DOMs is determined.
For example, if a todo has been marked as complete, the corresponding element in the Virtual DOM is updated to reflect this change.
Efficient Updates:
Instead of clearing the entire parent element and re-rendering everything, the Virtual DOM helps identify specifically what has changed.
Selective DOM Manipulation:
Only the elements that have changed are manipulated in the actual DOM.
This process is more efficient than a naive approach of clearing and re-rendering the entire DOM.
