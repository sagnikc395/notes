---
title: " Compilers Intro"
tags:
  - compilers
  - compiler-history
---
## What is a Compiler ?
- first need to understand what is an interpreter.
- program with low-level instructions are too hard for humans to understand and execute.
- typically what was done previously , people developed a new language , a new machine which executes on top of this low-level machine , it would be higher level than this lower level machine.
- Interpreter implemented using low-level isntructions, fetches the net instructions , interpreters and executes and move on to the new program.
	- Need some input data and generates some output.
- In a functional form:
	- Interpret :: (Program, Data) -> Output, output could be either a print stmt or something else.
	- Interpret -> implemented using low-level instructions 
	- Program -> high level instructions 
- LL(Interpret) :: HL(Program) -> (Data -> Output) i.e Currying the input
- Compile :: Program -> Executable 
- Executable :: Data -> Output


## Timeline of Compilers 

- What are the futures of compilers and why bother about studying for compilers.
- Past ?
	- how things evolve and likely to evolve in the future.

### Technology trends:
- Moore's law is running out of steam.
- Programming Language Abstractions are becoming higher level.
	- Gap between the abstractions and the hardware increases and compiler's job increases.

- Moore's Law -> Cofounder of Intel, (1965) , number of integrated components will double every year for at least the next decade -> exponential growth for the number of the components in the chip.
	- 1975 -> double every 2 years.
	- 2015 -> revised to every 2.5 years.
	- However speed saturated at around 2000s.

### Physical Limits to Transistor Scaling :
- Source-to-drain leakage
- Limited Gate Material
- Limited Options for transistor material
- Safe to assume that "all exponentials come to an end."
- Computers were just increasing in their speed,they started packing more and more cores on a single physical CPU and gave rise to multi-core computer.

### Architectural innovations Necessiated !
- single core cpu -> Multi core CPU.
- More SIMD (Single Instruction multiple Data) in Intel and ARM 
- Rise of GPUs that only implement SIMD abstractions -> particularly useful for graphics, deep learning and LLM models.
- Complex Instructions Sets Eg: x86-64 SSE, ARM SVE (scalable vector instructions),  basically allow parallel computations/ vector computations.
- Java/Python do not have abstractions that can abstract it in, onus is on the compiler to update it and map these efficiently onto the cores.

### Stumbling Blocks For architectural Innovations:
- stumbling blocks are blocked by compiler support.
- need compilers to provide first-class support for instruction sets -> not enough usage to justify the cost of developing them.
- Compilers havent been keeping pace.
- Compilers if improved -> can boost the entire computing ecosystem.
- Any improvements that being made, are likely to have a significant improvement in the future.

### Programming Language Abstractions 
- 2020s -> Tensorflow, WebAssembly, DryandLINQ
- 2010s -> Rust, Zig (C++ bad more focus on HPC in new languages, want both safety and performance), Typescript, Ruby ,Clojure 
- 1990s -> Python, Haskell, Java,R,Javascript (Mobility and code specificty, others are higher level)
- 1980s -> Matlab, C++,Erlang, Perl, Tcl
- 1970s -> C, SmallTalk, Simula, Prolog, ML 
- 1960s -> ALGOL, Simula, BASIC 
- 1950s -> Fortran, Flow-Matic, COBOL
- 1940s -> Assembly


### Early Adoption of Compilers:
- 1950s -> First language + compiler by John Backus 
- expert programmers thoughts it was too slow and not work and wanted to work in assembly.
- saw tremendous adoption by 1958.
- Most programms are now written in compiled or interpreted programming languages and have significantly improved -> far superior than the expert level code a assembly programmar would have written.

### Evolution of Compilers:
- Evolution of popular compilers:
	- GCC -> 1988 -2022
	- the number of lines of code in GCC is 20k * 1000 Lines of code.
	- Almost increased at a linear pace.
- Friendly competitior to GCC ,LLVM and optimized and code generates.
	- Grew at a steady rate and provides code optimizations for it.