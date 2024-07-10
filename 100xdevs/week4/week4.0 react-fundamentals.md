---
title: react-fundamentals
tags: react, frontend, fundamentals
---

- building blocks of a web application 
  - <em>user interface</em>
    - how users will consume and interact with our application
  - <em>routing</em>
    - how users will navigate between different parts of our application 
  - <em>data fetching</em>
    - where our adta lives and how does one get it 
  - <em>rendering</em>
    - when and where we render static and dynamic content 
  - <em>integrations</em>
    - what third-party services we use like CRM, auth and payments and how we connect to them 
  - <em>infra</em>
    - where we deploy, store and run our application code 
  - <em>perf</em>
    - how to optimize our applications for end-users
  - <em>scalability</em>
    - how does our application adapts as our team ,data and traffic grow
  - <em>devex</em>
    - experience building and maintaining our application 
  
- what is react ?
  - it is a JS library for building interactive user interfaces
  - by UI we mean the elements that users see and interact with on-screen
  - React is relatively unopinionated about other aspects of the build process. Results in may options to choose from, including Next

### what is next.js ?

- react framework that gives us building blocks to create web applications.
- next handles the tooling and configuration needed for react and provides additional structure,features and optimizations for our application.
- provides inbuilt routing, data fetching and caching -> all while improving the developer and end-user exp.


### rendering user interfaces (UI)

- when a user visits a web page, server returns a HTML file to the browser that looks like:
<img src="https://nextjs.org/_next/image?url=%2Flearn%2Fdark%2Flearn-html-and-dom.png&w=1920&q=75" width="500px" height="300px"/>

- DOM -> object repr of the HTML element. It acts as a bridge between our code and the user interface, and has a tree-like structure with parent and child relationships.

- we can use DOM methods and JS to listen to user events and manipulate DOM, by selecting , adding, updating and deleting specific elements in the user interface.

- DOM manipulation allows us to to not only target specific elements, but also change their style and content.

### updating UI with Javascript

- 