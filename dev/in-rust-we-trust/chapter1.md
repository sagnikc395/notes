---
title: getting our house clean
tags:
  - rust
  - PL
  - basic-programming
date: 21/6/25
---
### hello world 
- start by making a directory to store our Rust code.
- Make a new source file and call it main.rs. Rust files always end with the .rs extension. If we are using more than 1 word in our filename, convention is to use an underscore to seperate them.

### Anatomy of a Rust Program:
- main function is special. It always is the first code that runs in every executable Rust program.
- Function body is wrapped in {}. Rust requires curly brackets around all function bodies. It's good style to place the opening curly bracket on the same line as the function declaration, adding 1 space in between.
- println calls a Rust macro. If it was a function call instead it would be entered as println (i.e without the !).
	- using a ! means that we are calling a macro instead of a normal function and the macros don't always follow the same rules as functions.
- Secondly we pass the string `hello, world` as an argument to println! and the string is printed to the screen.
- Third, we end the line with a semicolon`;`, which indicates that this expression is over and the next one is ready to begin.

### Compiling and Running are separate steps
- Before running a Rust program, we must compile it using the Rust compiler by entering the rustc command and passing it the name of our source file.
- Rust is a ahead-of-time compiled language, meaning we can compile a program and give the executable to someone else and they can run it even without having Rust installed. 
- Just compiling with rustc is fine for simple program, but as our project grows, we will want to manage all the options and make it easy to share our code. 
- Everything is a tradeoff in language design.