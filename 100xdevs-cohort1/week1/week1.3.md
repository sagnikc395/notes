---
title: Async and Await Programming in Javascript
tags:
  - "#Javascript"
  - async-await
  - programming
---
# Async , await ,callbacks and Promises
- Might be confusing for folks and more asynchronous javascript.
- Callbacks , Promises and Arrow Functions.
- Very basic fundamentals and can get away with a lot of fullstack development without knowing these things, but helpful later down the line when require for actual development.
- Very basic fundamentals -> easier to spirt later if fundamentals are right.
### Asynchronous 

- **Async programming is a technique that enables our program to start a potentially long-running task and be able to be responsive to other events while that task runs, rather than having to wait until that task has been finished. Once the task has been finished , our program is presented with the result.**
- When we are doing long running tasks, if our task runs on the same thread as the other tasks, the long running task will block the thread and wouldn't let the other things work.
- reading of file out of control on node.js ;depends on the filesystem.
- setTimeout(callback,time); can define long running task defined on this; can defined tasks on the javascript tasks, setInterval etc are called as long running tasks 
- after sometime hello world came onto the screen.
- async functions are functions are long running functions that dont need the Javascript  main thread. They can be offloaded to other CPU cores and the Javascript thread can take back result and do something.
- Notice in stopwatch.js the synchronous code (the loop executes fast) and then interval is done.
- If we increase the counter by some huge value, the value will change to 1000_000_000 value.
- Javascript allows async task execution, but it can't do 2 or more things at a time. If right now, is what our JS code is doing, it will become idle as in what it is currently doing.
- Web Applications are highly async and they need to respond to HTTP requests and are all long running tasks and cant keep our thread blocked .

### JS Engine Working 
- ![[Screenshot 2024-04-27 at 10.45.21 PM.png]]


- Working of JS Engine  [Link](./jsengine.excalidraw)
- Refer to this online website for better and working understanding : 
- [Latent Philipe](http://latentflip.com/loupe/?code=JC5vbignYnV0dG9uJywgJ2NsaWNrJywgZnVuY3Rpb24gb25DbGljaygpIHsKICAgIHNldFRpbWVvdXQoZnVuY3Rpb24gdGltZXIoKSB7CiAgICAgICAgY29uc29sZS5sb2coJ1lvdSBjbGlja2VkIHRoZSBidXR0b24hJyk7ICAgIAogICAgfSwgMjAwMCk7Cn0pOwoKY29uc29sZS5sb2coIkhpISIpOwoKc2V0VGltZW91dChmdW5jdGlvbiB0aW1lb3V0KCkgewogICAgY29uc29sZS5sb2coIkNsaWNrIHRoZSBidXR0b24hIik7Cn0sIDUwMDApOwoKY29uc29sZS5sb2coIldlbGNvbWUgdG8gbG91cGUuIik7!!!PGJ1dHRvbj5DbGljayBtZSE8L2J1dHRvbj4%3D)
- It's waiting for its turn in the callback, and the event loop is fired , where the thing is free. 
- web apis are present outside of the js engine main thread and it tells it to put it outside of the javascript callback queue.
- The things are being polled onto the callback queue.
- The main engine is single threaded, (the code is occupied is very focuesed on the stack), JS call api is set on web apis.
- although the webapis are requesting our check , we are not adhering to their requests.
- Once we are finished checking from the callback queues, will we then only adhering to the callback queue and start pushing thing onto it.
-  async code cant block synchronous code, they can ping us , they can call us, but we will only do them when we are free which is from we are free from the call stack.
- only priority is synchronous code, async code is done by someone else. JS doesn't even run async code, it only runs synchronous code and it is given off to someone else.
- someone else here(web apis) are keeping a clock and telling javascript to do something.
- All fetch requests run on a different thread, running a video (encoding happens in different threads), js main thread is meant for simple things that the developers write and heavy compute and blocking requests are offloaded to different threads.
- Use of async code:
  - in chat.openai.com ; the ml model that runs and calculates the response is sent to the openai server and gives back the response.It could take 1s of it could take 100s. So long running and asynchronous.
- hence the fetch request is a async request. 
- main js threads will remain busy and the other part will remain and call to it.
### Callbacks :
- Any function that web apis(/called async) is called as callback.
### Promises :
- Very hard and need time to marinate.
- Promises will scare us as much as traits will be scary.
- No inherent need for promises in javascript , help write clean async code. 
- Abstraction over the callbacks hells and to prevent that , this was introduced. 
### Callback hell:
  - direct async call; ie. setTimeout , they all execute parallel and collected by main thread to display.
  - if calling one async call inside another, that will **chain** the async call.
  - The problem with async chaining here is that it looks ugly and when having a large number of such async calls we will have problems identifying the calls.
  - To solve this syntax problems, Promises were introduced. To make syntactically more easier and used throughout. 
  - Promise itself takes a function inside of it.
  - can call .then() function on it (i.e properties of the objects on it).
- Promise {<\pending>} is also an object. It has the properties of(most used) : - then, resolved, reject.
  - Javascript spec fold have now manadated that an async code bascially returns a promise.
  - It is a async function , but whenever we call it it will return us the Promise immediately and go on to do its task, rather than us giving its own callback.
  - In a callback , when we are calling a function , we tell the web api's that this is my callback, put them on call stack when done vs. when working with promisified code, they give us the promisified code immediately and immediately do something with this promise.
