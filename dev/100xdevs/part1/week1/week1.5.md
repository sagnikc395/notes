## Async Javascript , Real Use of Callbacks and JS Browser Architecture , Promises and Async - Await

- how does js work in the browser ?
- why async and await ?

- what does sync and async means ?

  - sync -> toegether, one after the other, seqeuntial i.e only one thing is happening at a time
  - async -> opposite of sync, happens in parts,
    multiple things are context switching with each other.

- Intuition of Async

  - humans brain and body is single threaded.
  - we can only execute one thing at a time.
  - but we can context switch b/w tasks, or we can delegate tasks to other people.
  - decrease the total time to execute some functions, single JS thread can delegate other "parts" to delegate to use other things.

Eg: file I/O is async by nature.

- Gist: even if you are single threaded, you can do things parallely by delegating. you can also context switch b/w tasks if need be(the net time to do both of the things would still be the same).

  - net amount of time taken to do a task can be decreased, by doing these two things (delegating and context switching).

### How does JS use async functions ?

- eg: setTimeout , setInterval is a asynchronous function.
- pre-made function js made for us available to use.
- what makes this async ?
  - when the pointer reaches the line on setTimeout funciton call, it does not wait for the function to complete before going to next line, rather pushes it into the stack.

### what are the common async functions ?

- setTimeout
- fs.readFile -> to read file from our filesystem
- fetch -> to fetch some data from an API endpoint

### How Does JS keep information about async functions ?

- callstack, webapis, callback queue and the event loop are high level thing make it asynchronous.
- callstack -> what is actually being put on the stack to actually been added. executed line by line and put on the stack
- webapis handles the async part, while the callstack executes the sync part line by line.
- while our thread is busy, we will ignore the elements in the callback queue and add the elements from the callback queue, when the main thread is free.
- the deal with event loop is its task to check if the main thread is free, its task is to put the elements from the callback queue and any other events if completed, and gets pulled from webapis -> callbackqueue -> callstack.
- callbacks only makes sense in async functions, in sync functions, they dont really make sense.

### Promises:

- Promises are syntactical sugar to make callbacks better.
- Also able to manage the callback hell, that is possible.
- most of the time all the async function that we will write will be on top of JS provided async functions like setTimeout or fs.readFile.
- callbacks do ugly things -> they do callback hell, the whole shebang about promise is to avoid this trap.
-
