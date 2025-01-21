## DOM Introduction

- Document object Model -> A standard for how to get, change, add or delete HTML elements.
- About :

  - Quick intro to DOM
  - How the DOM represents an HTML Document in memory ?
  - How to use APIs to create web content and applications .

- JS makes the HTML Page active and dynamic via the DOM.

### what is DOM ?

- A programming interface for web documents.
- DOM is not a programming language.
- Represents the page so that programs can change the document structure style and content.
- DOM is tree-like representation of the web page that gets loaded into the browser.
- DOM represents the documents as nodes and objects.
- Without it, the JS language wouldnt have any model or notion of web pages, HTML documents, SVG Documents and their component parts.
- Web API used to build websites.

### Accessing the DOM

- When we create the script, whether inline in a <\script> element or included in the web page, we can immediately begin using the API for the document or window objects to manipulate the document itself.
- The DOM was designed to be independent of any particular programming language, making the structural representation of the document available from a single,consistent API.

### DOM Tree:

- DOM is a tree-like repr of the web page that gets loaded into the browser.
- When a web browser parses an HTML document, it builds an DOM tree and then uses it to display the document.
- Let's look at the different objects:

  - Document Object -> Top most object in the DOM tree. It has properties and methods which we can use to get info about the document using dot notation.

- createElement() -> creates a specified elements and inserts it into the DOM.

```js
const para = document.createElement("p");
para.innerText = "This is a para";
document.body.appendChild(para);
```

### Finding HTML Elements:

- If we want to manipulate HTML elements, we first need to find the elements first. Multiple ways to do this:

  - Finding HTML elements by id
  - Finding HTML elements by tag name
  - Finding HTML elements by class names
  - Finding HTML elements by CSS selectors
  - Finding HTML elements by HTML object collections.

- getElementById():
  - Method to get an element from the document by its unique id attribute.
  ```js
  var firstDiv = document.getElementById("first");
  ```
- getElementByTagname():
  - Method to access one or more elements by their HTML tag name.
  ```js
  const divs = document.getElementByTagname("div");
  ```
- getElementByClassName():
  - Method to access one or more by their class name.
  ```js
  const x = document.getElementByClassNames("intro");
  ```
- querySelector():
  - finding HTML elements by CSS selectors.
  - can find all the elements that match the specific CSS selector.
  - It can be attribtue, value or any other type based too.
  - CSS selectros(id,class names,types, attributes,values of attributes, etc.) use the querySelectorAll() method.
  ```js
  var paragraphs = document.querySelectorAll("p");
  paragraphs.forEach((para) => (para.display = "none"));
  ```
  ```js
  var matches = document.querySelectorAll("p.intro");
  ```
  - querySelector() will only get the first one, while querySelectorAll() will try to get all of them.
- forms():

  - finding HTML elements by HTML Object Collections.
  - mainly in these case we can create a form element and get the items from them.

  ```js
  const x = document.forms["frm1"];
  let text = "";
  for (let i = 0; i < x.length; i++) {
    text += x.elements[i].value + "<br>";
  }
  document.getElementById("demo").innerHTML = text;
  ```

  - forms are not the only collection we can use, we have:
    - document.anchors
    - document.body
    - document.documentElement
    - document.embeds
    - document.forms
    - document.head
    - document.images
    - document.links
    - document.scripts
    - document.title

### NodeList vs HTMLCollection:

- NodeList:

  - returned by the querySelectorAll().
  - It is a collection of document nodes(element nodes,attribute nodes and text nodes)
  - Items can only be accessed by their index number.
  - Most often a static collection. Eg: if you add a <\li> element to a list in the DOM, the list in NodeList will not change.

- HTML Collection:
  - getElementsByClassName() and getElementsByTagName() methods return a live HTML Collection.
  - A collection of document elements.
  - Items can be accessed by their name,id or index number.
  - It is always a live collection. Ex: if you add a <\li> element to a list in the DOM, the list in the HTML collection will also change.

### Changing innerHTML:

- element.innerHTML -> Changes the inner HTML of an element.
- element.attribute -> changes the attribute value of an HTML element
- element.style.property -> change the style of an HTML element
- element.setAttribute(attr,value) -> change the attribute value of an HTML element.

### Dynamic HTML Content:

- document.write() -> writes directly to the HTML output stream.
- never use document.write() after the document is loaded. It will overwrite the document.
- setAttribute() method sets a new value to an attribute.
- If the attribute does not exist, it is created first.

- Adding and deleting elements:
  - document.createElement(element) -> create an HTML element
  - document.removeChild(element) -> removes a HTML element
  - document.appendChild(element) -> adds a HTML element
  - document.replaceChild(new,old) -> replace an HTML element
  - document.write(text) -> write to HTML output stream

### DOM Nodes:
- Entire document is a document node.
- Every HTML elements is an element node.
- Text inside the HTML elements are text nodes.
- All comments are comment nodes.
