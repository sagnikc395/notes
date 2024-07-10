---
title: Basics of Javascript
tags:
  - Javascript
  - programming
---
### Basics of Javascript
- JS is the most popular and most used programming languages and used .
- Entire applications are built around Javascript.
- Frontend developer, Backend developer and FullStack developer.
- For a long time JS was solely used in the browser to build interactive web pages.
- ~2008 , Ryan Dhall ported the v8 engine to a runtime, allowing it to run async code in the webservers.
- Web/mobile apps , real-time netwokring apps, games, and cli apps in Javascript.
- Browser has a JS engine to execute JS engine. (spidermonkey in firefox and v8 in chrome)
- Node is a C++ program that contains google's v8 engine.
- With Javascript can build the backend of our code in Javascript and Node.
- Javascript vs ECMAScript
  - ECMAscript is just a specification for Javascript and takes care of the ECMAScript specification.(1997 onwards,2015 annually)
  - ES2015/ES6 : -defined many new features for Javascript.

### Programming Languages:
  - 0s and 1s 
  - Assembly language 
  - High level programming languages.
  - Easy for computers,hard for humans , require higher level programming languages.
### JS Architecture:
  - ref: [JS Architecture Diagram](./js-architecture.excalidraw)
  - Needs to have content,some style and some funcitonality as well.
  - Need for this as scripting language for what we can do
  - HTML and CSS cannot do scirpting.
  - Back in the day, was made to only understood by browsers.
  - Every JS compiler need to follow the ECMAScript standard and on the js engines on it.
-  The things that interprets JS is very different for chrome,firefox and safari. All 3 of them have thier own engines, and wrote their own implementations of the ECMAScript standard.
-  The engine is responsible for making things from 0to 1 and that how things work.

## Node.js 

- ref: [Nodejs](./node-js.excalidraw)
- People realised that JS is a powerful programming language and has been running on the frontend , so we should also run them on the backend as well so as to quickly move teams and adopts things faster.
- Backend Machines:- A native program that is not on the browser(native apps).
- Node.js was one framework was that stripped from v8 engine (remote everything browser related) and just keeping the parts that was converitng javascript code to instructions.
- **Node.js -> runtime for Javascript.,just the engine that chrome use** 

## Primitives:
1. Variables 
2. numbers 
3. strings 
4. arrays  :- lets us iterate and store multiple data
5. loops :- helpful for iterating over things.
    - for 
    - while
6. Objects :- key.value pairs ; helpuful for modelling real world things
7. Functions :- primtiives ; passing functions inside functions ; takes a input , do some operations on it and returns a output.
8. DRY ; max reuse of code and can be reused freeely.
9.  Functions can take other functions as input. -> callbacks 

## Core Concepts of Javascript:
   
- single threaded 
- asynchronous
- loosely typed 
- interpreterd 
- native js vs apis
- Where can JS run:
  - browser 
  - data centers 
  - tvs 
  - mobile devices

### Single Threaded 
  - Cores of the machine -> no of cpus in the mahcine.
  - core is effectively a place where our code can execute.
  - core runs in a place line by line.
  - the more cores you have theretically more powerful your machine.
  - Node.js was written in a very shabby fashion, it works in a single core.
  - can't run multiple threads on it.
  - it was designed to be single threaded from scratch.
  - Hence, powerless language as compared to other.
  - Even if we try to distributing the thing by chunkifying the thing , we can't do that as the next one is blocked by the previos one to get fully processed as in as good as a serial processing itself.
  - If that could be done on parellelizing the thing, then could have processed it easily. single threaded  means one executore, so all jobs are executed sequencitally. cant delegate the thing or any side channels to distribute the load to multiple things.
### Asynchronous 
  - Javascript is asynchronous in nature.
  - or so do other tasks like file IO or any other task , sync code will block that code or file IO.
  - need to do complex tasks :- sending http requests, waiting for input, database writes etc. 
  - Something that needs to take time, async nature of JS is required.
  - Still running a single thread, this small task, send a message (promise) that will do it later.
  - async tasks do not work necessarily on the same thread as the main thread of javascript execution.
  - until that happens, we can still do the thing.
  - Once the file is read, can do whatever we want with the file.
  - eg: reading from the os is a complex task as our operating system is doing a bunch of things and machine does a bunch of things. And machine does a bunch of things, a request goes out and a response goes out.
  - if waiting for this to complete, then we are blocking on the thread here.
  - **To take the advantage of the async nature of JS, we need to use callbacks**.
    - a pass a function inside a function , sort of like a callback
  - Before file was reached ,the control read to the business logic for coding and we continued reading from the stream to get data.
  - Good thing about asynchronous tasks, the thread would have to wait. My CPU usage is low, until then do the other tasks, until then control logged to the screen and the thing went to other functions.
  - We can do heavy things offloaded by asynchronous programming while we do the easier things.
### Loosely Typed:
  - Types are loose in Javascript. it could be anything, made into anything. Source of lots of bugs , easier on development -> Typescript is the answer.
### Interpreted:
  - Executed line by line; not compiled into a machine language.
  - Easier and faster to develop and make applications to.
  - Execution speed becomes slow, a lot depends on JIT performance.
  - Compiled Languages will compile the Code to binary, process of pre checking , does a bunch of checks and error checks.
### Native JS vs Browser:
  - variables, loops,Date(), functions, objects, arrays etc.
  - fetch , setTimeout, setInterval -> Browser based APIs
  - different environments expose different APIs , Nodejs ,browsers, flights ,mobile etc.
