## Routing, prop drilling , context API

- Making simple projects dont really need routing and need to understand routing in react to make multi-page real-world applications.

- Jargon:

  - Single Page application ->
    - before react was a thing, we created website we added a index.html,index.js ... and loads the initial page.
    - if we change the route to /messages , pre -react days, it would send over another request and render the index.html
    - lead to a hard reload of a page and index.html comes and stuff will reload.
    - React will let us create Single Page Applications.
  - Client side bundling ->
    - bundle that we get from the backend.
    - final big JS file, all our pages that exist and etc. in a single JS file.
    - we get the single JS file from the server and do client side routing before knowing what the routing is.
  - Client side routing ->
    - React does client side routing.
    - only the first time we go to index.js , we load the initial load.
    - if we go to any other tab, there is no need for any other html,css ,js to come.
    - we have realistically a single page and changing the view somehow and rendering on the client somehow.
    - we can optimize our app, the part / unbundle that comes for that part, only that is loaded.
    - even as we change our pages, no other reload happens and client side routing happens.

- What are routes ?

  - In Express, we created the backend routes.
  - Rener a specific page , given a route -> render the specific route.
  - react-router-dom -> most popular one, router for dom.
  - same could be there for mobile, tv etc.
  - in react-router-dom , we have to define a group of routes and to create client side rendering to get the bundle once.

- Good question to have:

  - created a SPA with 2 pages -> home and navbar
  - we create a navbar at top for navigation for home and dashboard.
  - when we do create it , does a fresh index.html comes back from the server ? In client side routing it shouldnt create a fresh index.html and provide nav.
    - using window.location.href can be changed and make each page go to the ther page.
    - there is a flaw here:
      - In client side routing, if we change the page, we ge no html,js from the backend.
      - But here everything coming back again.
      - infact , there is some reloading happening here -> we actually not doing client side routing with this. -> not the right way to go from one page to other if we are doing client side fetching.
  - browser will think we need to refetch the data from index.html
  - we only want to react to fetch the data.

- the ans is to useNavigate() hook to navigate from one route to another.Simply changing the route and makes sure it is not doing a hard reload of the page, without keeping the same client bundle. Provided by react-router-dom.
- useNavigate() hook can only be invoked in a component, encapsulating BrowserRouter.
- also link wouldnt work if we automatically want to move a person to another page, useNavigate() will be required to use then.
- right method to do client-side routing.

- react-router-dom introduced lazy loading to only paritally load the bundle for that page. lazily load more components that the person in not currently on.

```jsx
const Dashboard = lazy(() => import("./components/Dashboard"));
```

- react provides the suspense api to render a fallback components, while the other component loads.
- so the previous comoponent can also be written as

```jsx
<Route path="/dashboard" element={<Suspense fallback={"loading..."}/>
<Dashboard />
</{Suspense}>
</Route>
```

### Prop-Drilling and Context API:

- how do you think one should manage stte ?
  - keep everything in the top level component (C1)
  - keep everything as low as possible (at the LCA of children that needs a state)

- push down state as down possible -> as to reload as few re-renders as possible.
- we can push the state down from App.jsx to lower level Feed and we always push down state as much as possible.
  - LCA -> lowest common ancestor(for 2 tree nodes, we need the state, we would store the state in their lowest common ancestor.)

- drilling down he props, withou explciitly passing by args everytime , as it becomes ugly down the line. It can just pass the props down the chain.
- Either way to manage state, we will need to drill the props down thorugh the component tree.
  - this will get very hard to maintain and highly verbose.
  - and this makes code highly unreadable.

- Prop drilling doesn't mean that the parent re-renders children -> it just means the syntactic uneasiness when writing code.

- Acc to official docs, passing props can become verbose and inconvinient when we need to pass some prop deeply through the tree, or if many components need the same prop. The neares common ancestor could be far removed from the components that need data and lifting the state up that high can lead to a situation called as "prop drilling".

### Context API
- Fixes the prop drilling issue.
  - It lets us teleport data to the tree that needed them without passing the props.
  - If we use the context api, we are pushing our state management outside of the core react components.
- things to learn:
  - createContext 
  - Provider 
  - useContext hook 

- contextapi is not for making your code performant, rather contextapi is for making the code prettier.
- 
