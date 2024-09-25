---
title: Better Programming Through OCaml
tags:
  - ocaml
  - functional-programming
  - cs3110
---
### Why OCaml ?
- Experience the freedom of immutability, in which the values of so-called "Variables" cannot change.
- Improve at abstraction, i.e the practice of avoiding repetition by factoring out commonality. 
- Exposed to a type systems which rejects the programs we think are correct. But we will come to love it, cause we will humbly realize that it was right and our programs were wrong.
- Exposed to the theory and implementation of programming languages, helping us to understand the foundations of what we are ssaying to the computer when we write the code.

### OCaml Background:
- It originates from the work done by Robin Milner and others at the Edinburgh Lab for Computer Science in Scotland.
- They were working on theorem provers in 70s and 80s. Traditionally , theorem provers were implemented in languages like Lisp. Milner kept running into the problem that the theorem provers would sometimes put incorrect "proofs" together and claim that they were valid.
- He constructed ML -> Meta Language. The type system of ML was carefully constructed so that we could only construct valid proofs in the language. A theorem prover was then written as a program that constructed a proof.
- In the 80s, the ML community divided into OCaml and Standard ML. MSFT also introduced its own variantof OCaml called F#.

### OCaml Current:
- OCaml is a functional programming language.
- Key linguistic abstraction of functional languages is the mathematical function.
- A function maps an input to an output, for the same input , it will always produce the same output.
- I.e the mathematical functions are stateless -> they do not maintain any extra information or state that persists between the usages of the function.
- Functions are first class -> we can use them as input to other functions and produce functions as output.
- Expressing everything in terms of functions enables a uniform and simple programming model that is easier to reason about than the procedures and methods found in other families of languages.

#### Mutability:
- Fantasy of mutability in imperative languages like C and Java is that it's easy to reason about -> machine does this,then this etc.
- Reality of Mutability is that whereas machines are good at complicated manipulation of state, humans are not good at understanding it. Essence of that is mutability breaks referential transparency.
	> the ability to replace an expression with its value without affecting the result of a computation.
	
- In reality, there is no single state , computer systems go to great lengths to provide that illusion. In reality, there are many states spread across threads, cores processors and networked computers. And the machine does many things concurrently. Mutability makes reasoning about distributed state and concurrent execution immensely difficult.
- Immutability fress the programmer from these concerns. It provides powerful ways to build correct and concurrent programs. OCaml is primarily an immutable language, like most functional languages. It does support imperative programming with mutable state.

### OCaml Features:
- Statically typed and type-safe programming language.
- Statically typed language detects type errors at compile time, if a type error is detected, the language wont allow execution of the program.
- A type-safe language limits what kinds of operations can be performed on which kinds of data.
	- This prevents a lot of silly errors -> i.e treating an integer as a function and also prevents a lot of security problems -> over half of the reported break-ins at the CERT were due to buffer overflows, something impossible in a type-safe language.
- C/C++ are statically typed but not type-safe -> they cehck for some type errors, but don't gurantee the absence of all type errors. That is, there is no gurantee that a type error won't occur at run time. Other languages like Java use a combination of static and dynamic typing to achieve type safety.
- Other advanced features in OCaml:
	- **Algebraic Data Types** -> Can build sophisticated data structures in OCaml easily , without fussing with pointers and memory management. Pattern matching -> enables examining the shape of a data structure -> makes them even more convinient.
	- **Type Inference** -> We don't need to write type information down everywhere. The compiler automatically figures out most types. This can make the code easier to read and maintain.
	- **Parametric Polymorphism** -> Functions and data structures can be parameterized over types. This is crucial for being able to re-use code.
	- **Garbage Collection** -> Automatic memory management, relieves us from the burden of memory allocation and deallocation.
	- **Modules** -> OCaml makes it easy to structure large systems through the use of modules. Modules are used to encapsulate implementations behind interfaces. OCaml also provide functions (functors) that manipulate modules.

### Future Trends:
- A good programmer has to learn the principles behind programming that transcend the specifics of any specifc language.
- Learning a new language from scratch affords the oppurtunity to reflect along the way about the difference between programming and programming in a language.
- OCaml does a great job of clarifying and simplifying the essence of functional programming in a way that other languages that blend functional and imperative programming(Scala) or take functional programming to the extreme(Haskell) do not.
- Advanced features of functional languges have a surprising tendency to predict new features of more mainstream languages.
	- Java has garbage collection in 1995, Lisp had it in 1958.
	- Java got generics in 2004, ML had it in 1990.
	- First class functions and type inference were long present in functional languages before more mainstream programming languages.

