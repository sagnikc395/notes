## Javascript Foundation

### why languages ?

- need to represent logic for human understandable thing and to make it easier for us to program and to effectively program from a higher level representation to a lower level representation.
- everything will actually go to 0s and 1s into the RAM.
- the compiler/interpreter will convert from a english like syntax to 0s and 1s.
- developers are very dumb and require a high level representation and want a high level programming language to convert the code.
- Languages are all written to write large scale software applications.

### Interpreted vs Compiled Languages

- compilers convert high level developer friendly code into 0s and 1s.
- things that we can write in plain english.
- C++ is a compiled language -> high level lang -> binary ; i.e compilation + linking required.
- JS is interpreter -> just run node \<file-name> , can simply directly run this code. A specific compilation step is not required.
- It is going line by line, it does not care about specific steps.
- Compilation does not happen, if there is an error in the code, while in interpreted we can run line by line, can run partially if the error comes later.

### Why JS >> other languages in some use-cases

- browsers can only understand HTML/CSS/JS(for most of the cases)
- thanks to nodejs , JS can also be used for "Backend Development"

### Strict vs Dynamic Languages

- C++ has very strict types i.e during compilation a lot of bugs can be eliminated from the types itself, while in JS, each binding can take any type of value.
- JS is loosely typed -> allows us to change types of varibales -> not great, it will create a bunch of runtime errors later down the line.

### Single Threaded Nature of JS

- Go, C++ etc are multi-threaded , while JS, Lua etc. are single threaded.
- Cores means -> 1 single core, can run a single core at the same time.
- 1 single core can only run 1 thing at time, the more number of cores we have, the more number of processes we can have.
- JS is always restricted to a single core, cannot decrease the load across the cores and to optimize the time to run it.
- However, there ware ways to make it use all cores in out machine.
  - nodejs workers / cluster module.
- JS runs line by line and only one line runs at once.

### Simple Primitives in JS(Numbers,strings, booleans)

- variables(let,var,const)
- data types -> strings, numbers and booleans
- if/else
- loops -> for loops

### Complex Primitives in JS(Arrays,Objects)

- arrays and objects
- to hold more data and varying types.
- objects store values in the form of key value pairs in JS.

### Functions in Javascript

- they allow us to abstract out logic in our program.
- take arguments as an input
- return a value as an output
- we can think of them as an independent program that is supposed to do something given an input
- Functions can take other functions as input -> callbacks

### Practice Problem Solving

### Callback functions,Event loop, Callback Queue, Async programming

- functions insides functions, and functions passed into another functions.
- setTimeout

  - inbuilt function baked into browser and node
  - second argument -> number of milliseconds we need to wait before the first argument runs
  - first arguments can be any expression.

- us passing functions to values as methods is also callback.

- setInterval
  - same like setTimeout, execept that is calls after some intervals.

### Callback hell and Promises.
