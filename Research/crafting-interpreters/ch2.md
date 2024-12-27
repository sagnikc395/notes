---
title: Map of the Territory
tags: 
date: 27/12/24
---
## Parts of the Language:

### Scanning:
- Scanning also known as lexing or lexical analysis. 
- Scanner takes in the linear stream of characters and chunks them together into a series of something more akin to "words". In programming languages, each of these words are called as token.
- Some characters in a source file doesnt actually mean anything. Whitespace is often insignificant and comments, by definition are ignore by the language.
### Parsing:
- Where our syntax gets a grammar - the ability to compose larger expressions and statements out of smaller parts. 
- Parser takes the flat sequence of tokens and builds a tree structure that mirrors the nested structure of the grammar. These trees are also called as parser tree or abstract syntax tree - depending on how close the bare syntactic structure of the source language they are.
- Parsers job also include letting us know when we do by reporting syntax errors.

### Static Analysis:
- Now the individual characteristiscs of each language start coming into play. At this point,we knwo the syntactic structure of the code - things like which expressions are nested in which, but we don't know much more than that.
- First bit of analysis that most languages do is called binding or resolution.
	- For each identifier, we find out where that name is defined and wire the 2 together.
	- This is also where scope comes into play - the region of source code where acertain name can be used to refer to a certain declaration.
	- If the language is statically typed, this is when we also do the type checking. Once we know where a and b are declared , we can also figure out their types. Then if the types don't support being added to each other, we report a type error.
- Now all this semantic insight that we gained needs to be stored somewhere. There are a few places that we can squirrel it away:
	1. Store it right back as attributes on the syntax tree itself -> extra fields in the nodes that aren't initialized during parsing but wll get filled in later.
	2. Store the data into a lookup table off to the side. Typically, the keys to this table are identifiers -> names of variables and declarations. In that case, we call it as a Symbol table and the values it associates with each key tells us what that identifiers refers to.
	3. One of the best ones it to transform the tree into an entirely new data structure that more directly expresses the semantics of the code.

### parsing, scanning and static analysis are considered the front end of the implementation.

### Intermediate Representations:
-  In the middle , the code may be stored in some IR that isn't tightly tied to either the source of destination forms. Instead , the IR acts as an interface bw these two languages.
- This lets us support multiple source languages and target platforms with less efforts. 
- A shared intermediate representation reduces the effort to full end to end compilers as you can practically abstract away the frontend and the backend for each target architecture. We can now mix and match these to get every combination.

### Optimization:
- Once we have understood what the user's program means, we are free to swap it out with a different program we can optimize it.
- Eg:1 Constant folding -> if some expressions always evaluates to the exact same value, we can do the evaluation at compile time and replace the code for the expression with its result.
- Optimization is a huge part of the programming language business. Many language hackers spend their entire careers here, squeezing every drop of performance they can out of their compilers to get their benchmarks a fraction of a percent faster. It becomes sort of a obsession.
- However in the real world, many successful languages have relatively few compile-time optimizations. Eg: Lua and CPython generate relatively unoptimized code and focus most on their performance effort on the runtime.

### Code Generation:
- Last step is converting our program to a form that the machine can actually run on. In other words, generating code(or code gen) , where "code" here means primitive assembly-like instructions a CPU runs.
- Back-end of the stack, descending the other side of the mountain. From here on, our representation of the code becomes more and more primitive. 
- Here we have a decision to make. Do we generate instructions for a real CPU or a virtual one ?
	- If we generate real machine code, we get an executable that the OS can load directly onto the chip.
	- Native code is lightning fast, but generating is a lot of work.
	- Speaking the chip's language also means that our compiler is tied to a specific archtiecture.
- To get around this, Martin Richards and Nikalus Wirth and more, made their compilers produce virtual machine code. Instead of instructions for some real chip, they produced code for a hypothetical ,idealized machine.Also called as bytecode because each instruction is often a single byte long.
	- These synthetic instructions are designed to map a little more closely to the language's semantics , and not be so tied to one computer architecture and its accumulated historical cruft. We can think of it like a dense,binary encoding of the language's low-level operations.
### Virtual Machine:
- If out compiler produces bytecode, our work isnt over once that is done. Since there is no chip that speaks that bytecode, it's our job to translate. 
- Here also we have 2 options:
	- we can write a little mini-compiler for each target architecture that converts the bytecode to native code for that machine.
		- we still have to do work for each chip that we support, but this last stage is simple and we get to reuse the rest of the compiler pipeline across all of the machines we support.
	- Or we can write a **virtual machine** , a program that emulates a hypothetical chip supporting our virtual arhcitecture at runtime. Running bytecode in a VM is slower than translating it to native code ahead of time because every instruction must be simulated at runtime each time it executes. It return we get simplicity and portability.

### Runtime:
- If we have compiled it to machine code, we simply tell the operating systems to load the executable and off it goes.If we compiled it to bytecode, we need to start up the VM and load the program into that.
- The GC goes into the runtime , if the language supports garbage collection.In a fully compiled languge, the code implementing the runtime gets inserted directly into the resulting executable.If the language is run inside a interpreter or VM, then the runtime lives there.

## Shortcuts and Alternate Routes:
### Single Pass Compilers:
- Some simple compilers interleave parsing,analysis and code gen so that they can produce output code directly into the parser, without ever allocating any syntax trees or other IRs.
- We have no intermediate data structures to store the global information about the program, and we dont visit any previously parsed part of the code. This means as soon as we see some expression, we need to know enough to correctly compile it.

### Tree Walk Interpreters:
- Some programming languages begin executing code right after parsing it to an AST. To run the program , the interpreter traverses the syntax tree one branch and leaf at a time, evaluating each node as it goes.
- This is very common for student projects and little languages, but not widely used for general purpose languages, since it tends to be slow.

### Transpilers:
- This are called as source-to-source compiler or a transcompiler. In this we convert the front end of our language to the back end instead of doing all the work to lower the semantics to some primitive target language, we produce a string of valid source code for some other language, that is about as high level as ours.
- Most transpilers today work on higher level languages. After the viral spread of UNIX to machines various and sundry, there began a long tradition of compilers that produced C as their output language. C compilers were available everywehre UNIX was and produced efficient code, so targeting C was a good way to get our language running on a lot of architectures.