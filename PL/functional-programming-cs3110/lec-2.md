---
title: Basics of OCaml
tags:
  - ocaml
  - functional-programming
  - cs3110
---
### Basics of OCaml 
- First let's think about a bigger idea -> learning languages in general.
- There are 5 essential components to learning a language -> syntax, semantics, idioms, libraries and tools.
	- **Syntax** -> 
		- we mean the rules that define what constitutes a textually well-formed program in the languge, including the keywords, restrictions on whitespaces and formatting, punctuations,operators etc.
		- The syntax can feel odd compared to languages we already know.
		- But the more languages that we learn, the more we become used to accepting to the syntax of the language for what it is, rather than wishing it were different.
		- We need to understand syntax just to b able to speak to the computer at all.
	- **Semantics** ->
		- We mean the rules that define the behaviour of programs.
		- Semantics is about the meaning of a program - what computation a particular piece of syntax represents.
		- There are 2 things to semantics ->
			- Dynamic Semantics:
				- defines the run-time behaviour of a program as it is executed or evaluated.
			- Static Semantics:
				- Defines the compile-time checking that is done to ensure that a program is legal , beyond any syntactic requirements.
				- Type checking -> rules that define whether a program is well-typed or not.
				- We need to understand semantics to say what we means to the computer and we need to say what we mean so that our program performs the right computation.
	- **Idioms** ->
		- Common Approaches to using language features to express computations.
		- Given that we might express one computation in many ways inside a language, which one do we choose ?
		- Programmers who are fleunt in the language will prefer certain modes of expressions over others. 
		- We could think of this in terms of using the dominant paradigms in the language effectively, whether they are imperative , functional ,object-oriented etc.
		- We need to understand idioms to say what we means not just to the computer but to other programmers as well.
		- When we write code idiomatically, other programmers will understand our code better.
	- **Libraries** ->
		- They are bundles of code that are prewritten for us and can make us a more productive programmer , since we wont have to write the code ourself.
		- Part of learning a new language is discovering what libraries are available and how to make sue of them.
		- A language usually provides a standard library that gives us access to a core set of functionality, much of which we would be unable to code in the language itself like file I/O.
	- **Tools** -> 
		- minimally a compiler or interpreter is provided.
		- But there are other kinds of tools -> debuggers, IDE and analysis tools for things like perf,memory usage and correctness.
		- Learning to use tools that are associated with a language can also make us a more productive programmar.

### OCaml TopLevel:
- Top-level is a calculator or a CLI. Toplevel is handy for trying out small pieces of code without going to the trouble of launching the OCaml compiler.
- However for large programs, compiling, creating and testing large programs will require more powerful tools.
- Also called as REPL -> read-eval-print-loop.

### Types and Values:
- In utop, we can end an expression with a double semicolon and press return key. OCaml will evaluate the expression , tell us the resulting value and the value's type.
- 