---
title: todoapp,mui,flexbox,basic state management
tags:
  - react
  - user-interface
  - css-flexbox
---

- need to move over this bump is react and understanding the great start. we incrementally build up and it is a good starting point.
- in react there are components:
	- defining our own html tags.
	- effectively created our new HTML tag which returns the html stored .
	- Components are used to abstract a lot of HTML together.

### components:
- think of components, as yourself defining your own HTML tags and the HTML tag sort of returns all of the HTML.
- they are a way to abstract a lot of HTML together.
### props:
- arguments , that can dynamically sent to a component that can be rendered.
- Ideally should put majority of code in different compoenents and keep components logically seperate.
### css :
- can pass css directly in our components using double braces.
- can send data to components and also used it inside our components.
- vw -> complete view width 
- vh -> complete view height 
- box with all input boxes -> Card.
- in the industry, most of the times, we use templates/ frameworks to use those components to make products faster and to not write a lot of better ourselves.
### flexbox:
- common thing to keep things in center.
- basically to position things to various positions of the screen.
- natural progression after center ; not to make elements take the full width and to position them in one of these positions.
- also requires some grasping.
- flex work only on one -leve, the grandchildren wudlnt be flex unless the children are also in flex.
- divs take by default whole width, span can be used.
- real world to restrict the width of things using flexbox.
- know elements shouldnt take full width , use flexbox.
- the parent div , give display: flex , to introduce flexbox.
- justify-center
	- if start ; then everything appears at the start.
	- if end ; then everything appears at the end.
	- space-between ; 3 elements equally spaced.
 - if we have added flex to a parent doesn't mean its grandchild also will have that, check the most immediate parent tag property. only works in 1 level.
### routing:
- we want user to click a button and conditional render component based on that .
- few ways to do it ; native way to do it using state management.
- external routing libraries are also present.
- routing to a path when redirecting a component.
- if path is / then render component1, else render component2 etc.
- conditional rendering.
- these routes are usually defined in one file.
- to add a new page is to add a new route.
- the router can work inside the scope of other elements in it as well.
- the code will change based on the route it is based on it.
- generally we can keep the routing route in the appbar and is present in each page for easy navigation.
- can directly route using window.location 
- however this can cause a full reload.
- single page application, keeps the structure intact and doesn't need full reload of the data, shouldnt need to do it.(window.location does that)

- problem with window.location -> a full reload of the page happens, but generally these creates good spa -> structure of the page changes but the structure shouldnt go away. 
- window.location -> moves the page to new page.
- we want the routing without reloading the entire page.