---
title: Basics of Monkey Interpreter
draft: "true"
tags:
  - interpreter
  - golang
date: 12/7/24
---
   
- Basics of the Monkey programming language and interpreter:
	- An interpreter is built to interpreter a specific programming language. That's how we implement a programming language. Without a compiler or an interpreter a programming language is nothing more than an idea or specification.
- Expressed as a list of features, Monkey has following features:
	- C-like syntax 
	- variable bindings 
	- integers and booleans 
	- arithmatic expressions 
	- built-in functions 
	- first-class and higher-order functions 
	- closures 
	- a string data structure 
	- a array data structure 
	- hash data structure

- Major parts of the interpreter will be the following parts:
	- lexer 
	- parser 
	- Abstract Syntax Tree (AST)
	- internal objet system 
	- evaluator 

- 