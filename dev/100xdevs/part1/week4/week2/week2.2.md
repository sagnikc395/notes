## week2.2 | Express and Backend Development

- Nodejs runtime , HTTP and how does it work.
- HTTP protocol and how to communicate between frontend with backends.
- building HTTP servers.

### Nodejs and its runtime :

- ECMAScript / Javascript ?

  - ECMAscript is a specfication based on which JS is based upon.
  - Every new things, new things are added, the compiler should support.

- What is Javascript ?

  - Is the implementation of the ECMAScript in the browser. Mostly used and widely known specification of ECMAScript.
  - Different specification are there, need a bundler to roll down new changes to old version for old browsers.
  - DOM is not part of the ECMAScript specification , but part of JS.
  - setTimeout,setInterval etc. also part of it.

  - Common JS runtimes:
    - V8 -> Google Chrome (c++) -> converts JS into binary -> open source -> JIT Compiler for JS
    - SpiderMonkey -> Firefox (c++,rust) -> converts JS into binary

### Nodejs

- some people realized that some parts of the js engines can be extracted and run as a runtime for the JS. (2011-12 ish)
- take v8 engine, add some extra functionality on top of it and make it a backend language.
- its a JS runtime, that can run JS code .

### Bun

- Bun is a Javascript runtime , which is written in Zig, it is significantly faster than the Nodejs runtime.
- eventually , people will move to this as it has excellent backward compatibility with nodejs

### What can we create with Nodejs ?

- CLIS
- create a video player
- create a game
- create an HTTP server -> most of the time we make use of this.

### what is an HTTP server ?

- Protocol -> set of rules that both the parties know on how to talk to each other.

- HTTP:(Hypertext Transfer Protocol)

  - a protocol that is defined for machines to communicate.
  - specifcially for websites, it is the most common way for our website's frontend to talk to the backend.

- basically machines talking to each other.

- Frontends:

  - just the frontend and UI
  - also called as clients.

- Backends:

  - write servers, business logic and connect with the servers.

- fullstack :

  - frontend + backends

- 90% of the time protocol used is HTTP, sometimes else like websockets(continuous changing backend apps) or webrtc(yt)

### HTTP protocol gist

- Client throws some information at a server
- server doing something with that information
- server responding back with the final result

- think of them as function where :

  1. arguments are something that the client sends
  2. rather than calling a function using its name, the client uses a URL.
  3. rather than the function body, the server does something with the request.
  4. rather than the function returning a value, the server responds with some data.

- think of HTTP as RPC(remote procedure calls) -> we call then remotely residing over a server.

### Things client needs to worry about :

- what protocol they are exposed on -> HTTP/HTTPS(secure version)
- address/URL of the backend server
- IP/Port
- Route / Headers/ Body/ Query Parameters
- Methods

### Things server needs to worry about :

- respons handlers
- response body
- status codes

### URL has a few parts:

- Protocol -> http:/ https:/
- domain -> chat.openai.com
- route -> /backend.api/conversation

### body :

- arguments that we send to the server.
- i.e message to be sent to the openai server

### method :

- what action we want ?
- get, put,post,delete etc.

### status code, responsebody, response header :

- status code -> what is the status server responds with
- response body -> the output
- response header -> header response that we are getting

### Lifecycle when we fire the request in a browser:

- Browser parses the URL
- Does a DNS lookup -> convert domain name to a IP
- establishes a connection to the IP -> handshake

- DNS Resolution / Lookup ?
  - URLs are just like contact list on phone.
  - kv pairs of name to number
  - here in the end map a string(domain name) to an IP.
  - if we ever buy a URL of our own, well need to point to it to the IP of our server.

### Express , post and get requests and sending data via body:

- amongst data that went out is a cookie that went out.
- express does not handle the body of the response, rather hands it over to another thing to handle the body. use body-parser.
- using bodyparser as a middleware i.e whenever body has some json , it will first pass on the bodyparser , which will parse the json first and then handle to the get.
- can use nodemon to provide hot reloading.
- fetch is a webapi , async that allows us to fetch some details from a remote.
- anytime a request that comes /asd , return hello world.
- each process binds itself to a part, and when we send a request, it starts from the default port.
- payload is the meat of the thing that we want to send to the backend api endpoint.
- whenever we are setting server we can lock our server with the given server and set cookies accordingly.
- to send body in the browser, we send using the query parameters using like ?message=123
- body-parser module enables us to parse incoming request bodies in a middleware. Express.js server needs to know what type of data we are sending over the network, so it knows how to parse it.
