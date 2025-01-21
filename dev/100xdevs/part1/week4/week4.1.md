## DOM Introduction:

- What are we covering ?

  - DOM, Dynamic Frontends, Connecting FE to BE
  - Chrome Dev tools, why frontned frameworks.

- DOM(Document Object Model) API is a programming interface for web documents. It represents the page so that programs can change the document structure, style and content. The DOM represents the document as a tree of objects -> each object represents a part of the page.

- Before DOM:
  - JS was an implementation of the ECMAScript spec.
- setTimeout , setInterval etc. are some browser specific functionality provided by browser on top of vanilla ECMAScript spec, similarly for Nodejs.

### DOM project:

- create a simple website to calculate the sum of 2 user input numbers.
- This is a static website, clicking the button does nothing.
- Making the website dynamic:

  - Changing the elements on the website when the website is loaded.
  - Actualy calculating the sum based on the inputs and rendering it on the screen.

- Classes and Ids in HTML:

  - class helps in dry principle -> can define a style and replicate across elements and make them.
  - class is very commonly used primitive and used throughout in old codebases (before React).
  - id are supposed to unqiuely identify a element. We generally avoid attaching the same id to multiple elements. It also also be used for style.
  - avoid having same id for several containers.

- why are ids useful ?
- classes let us get rid of code repetition, but what do ids do ?

  - they let us access elements via the DOM API.
  - Can we use these IDs to CSS ?
    - Yes
  - But what do we use it for Usally ?
    - JS

- DOM is the global variable using which we can manipulate the HTML page using Javascript.

- Now assume that you dont have access to the calculation logic on the frontend. Lets assume its a hard problem that someone has exposed on a backend server ,and you need to hit the backend server and get back the value.

**Assignment**:

- Similarly we can build the same project for building a si calculator, given a principal, rate and duration return a response object with interest amount and the final amount. Also get rid of the button when any one of the value changes.

### Throttling or Debouncing:

- Our Frontend here , anytime we are changing the value, a request is going out.
- anytime a input changes, call the populateDiv function, and if we change the first or second one , the request goes out.
- The problem is the number of requests are increasing while it should have only been one. Optimize them so that so many requests dont go out.
- Debouncing -> you dont send out request immediately as user is typing, we slowly ease into it and send over say like 100ms delay.
- i.e delayed sending out of requests.

- define another function debouncedPopulatedDiv() , supposed to call populateDiv, if this not called for 100ms.
