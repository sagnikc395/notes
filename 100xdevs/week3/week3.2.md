---
title: foundations of frontend
tags:
  - frontend
  - jsdom
---

- understanding reconciliation in react and diving into legacy frontends(until 2014)
- why react, vue and other were introduced as frameworks , and what was the problem faced with vanilla frontend development.
- Why learn this and learn foundations ?
	- Good for foundations  -> depth of knowledge
	- Knowing about reconciliation and knowing about internal working on stuff and learn fundamentals properly.
	- Knowing stuff like this would enable you to get into specialist roles.
- Dynamic Website :
	- know all of the html and the pairs before hand 
	- data not coming from backend and not having a HTML upfront and once it comes we need to insert a HTML 
	- very similar to what data is coming and need to slowly insert it into the DOM.
- DOM Object :
	- programmatically insert into DOM objects using document.createElement(\<element type>), this wont be added to DOM, add to DOM and then add html using innerHTML property.
	- and can add child element using appendChild() method and insert div inside another div.
	- for the longest time, we were writing this long amount of code, to add some minimum functionality on the DOM and make changes on it.
- What is reconciliation ?
	- putting stuff on dom , being explicit , remove etc. done till 2014, is very repetitive and boring.
	- createChild,appendChild and removeChild etc are methods that are done under the hood for any website.
	- frmaeworks like react and vue hide these complexity.
	- here we only have to care about only putting the right thing in the right varibale and only care about converting one state to another in there.
	- taking the update of the state and translating into dom using updatechild and removechild.
- creating a reconciler of our own ?
	- function (todos) and creates the right things here.
- if in react , if the state ever changes, it compares the difference of the DOM , and only applies the changes of the DOM.
- do a parentElement.removeChild() and remove the element from it.

### send the right todo and the right description 
- each of these input boxes we are using some way to capture the user information from the user and rendering it on the UI.
- Inside JS , we can get the input in the input box using document.getElementById("title").value;
- server can get the right todo and get the right item using the getElementById to fetch the right details.


## dom manipulation 
- websites are dynamic , we also dont know the HTML upfront and have to generate the HTML on the fly.
- to make HTML on the first get, it wont be pre rendered it will come from back.
- dynamic website -> we dont know the HTML upfront and we have to render the HTML on it.
- POST request sends the data to the data to be sent.
- To dynamically add new elements using Javascript:
	- add item to the innerHTML by calling the JSON.stringify method on it.
- Use Javascript to create HTML.
- to create a new element:
	- const a = document.createElement("div");
	- to change the innerHTML, simple assign to the a.innerHTML property of it.
- similarly we can programmatically add another childElement inside the parent div and add new element on it.
	- using parentElementname.appendChild(childElementname) into it 
- similarly we can go another level deeper and add more children.
- this is what actually happens inside HTML.
- we can programatically do this 
	- called as DOM manipulation
	- dynamic websites created like this for the longest time

### what is reconcilation ?
- writing this much boilerplate code should be illegal.
- we are writing a lot of code for doing something so simple.
- everything happens under the help with DOM.
- React and Vue came to hide this complexity. 
- For us the developers we need to only need to care about the state in JS.
- that figures out what needs to add , what needs to delete etc.
- 