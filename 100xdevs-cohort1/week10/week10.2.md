---
title: Nextjs Introduction
tags:
  - nextjs
  - react
  - user-interface
  - ssr
---
## why next, and why is it so popular ?
- Server Side Rendering/ Netxtjs might sound like buzzwords as a popular library.
- 3 broad things, that are real world shortcomings that Next was made to solve:
	- Waterfalling 
	- Not SEO Optimized.
	- Doesnt work in places JS can't run(emails)
	- money churning thing for nextjs and they can monetize on that.
- Solution:
	- Server Side Rendering 

### Reasons:
- **Waterfalling**
- In React when we go to a website, we hit the server (CDN) and get a HTML with a JS script tag, which is a very big JS code.
- In real world, first request goes , it gets the HTML (rendering the skeleton) and then fetches the Javascript and then we hit the backend server to get user details and when we get the user details we render them on the screen. Till then it is just a flash for just a second.
- 
![[Screenshot 2024-07-03 at 11.56.55 AM.png]]

- This thing is called waterfalling -> for a few ms the white screen is rendered, then the UI skeleton in HTMl loads and then the JS loads. We have to wait round trip time for it to complete before it can render it on the browser.
- Very Unoptimal for production level apps and it would cause issue.
- **SEO Optimization is not there in React**. 
	- When Google and Bing scrape the websites, they scrape the HTML and CSS only and get the data, but React code mainly serves the JS files, search engines dont run JS and want to get information about this website. Search engines are not properly indexing them.
- **React will not work in a place where JS doesnt work** ->
	- Email providers wont let end users(like companies ) to render JS sent on email attachments for security reasons. 

### SSR:-
- Server Side Rendering -> react is great , and when the first render happens, instead of doing that in client, do that on server and the future renders can happen on client.
- cal.com has a emails package. It takes a React component as input and render that to static markup (HTML) and sends that to the end client -> React DOM Server.
- this works well if we only want a single render of our code to a static markup to render the Javascript.
- React -> single App.jsx file -> build -> link to the JS File -> SPA file 
- SSR ->
	- React -> App.jsx -> build for the first component to Static for the first render.
- All following rendering because of state updates happens on client.
- can use other server components, divs and spans.
- can import libraries only on the server to keep small bundle size.
	- nextjs can check what is required on the server and on the client side.
- Have complete access to the backend.
- can read from a file.
### How can we do it ?
- we want a website that is intially server side renderd and then on future events, should render on the client.
- the initial render should be well hydrated in the server itself.
- so the client bundle still exists ,but intiially it will have the markup prehydrated for the first load.
- in the backend, we can run the backend server for reuqests, one backend (for rrendering) and even connection to the database , it can be written in a single file , reducing the amount of code needed to be written.
- Everything happened in the same server therefore reducing the latency.

### Facts about Next.js /SSR:
- No access to browser consturucts(localStorage,window)
	- get back response in our browser.the JS that is running, during hydration, cannot use localStorage as that runs in the backend.
- Can't run hooks, doesnt understand state.
- Only renders once(the first time) on the server,future rendering (based on state change) happens on the borowser.
- Also lets us write HTTP backend routes(no need for express)

### Folder Structure:(Next 13)
- /pages 
	- /signup
	- /signin 
- /index.ts -> landing component code written here.
- to create a page /course/:cousrseId -> /pages/course/index.tsx is the first page that will get served at that folder.


- check the network tab and the first page load, different from react code . a lot of the code is already present in the initial HTML page load.
- 