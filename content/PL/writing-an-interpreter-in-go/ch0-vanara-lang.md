---
title: Specification and Requirements of the Vanara Programming Language
tags:
  - PL
  - interpreter
  - vanara
  - language-specification
date: 24/5/25
---
### Idea:

- Building a tree-walking simple interpreter. Building our own lexer, parser, our own tree representation and our own evaluator.

### Language Spec.:
- Every interpreter is built to interpret a specific programming language. That's how we implement a programming language.

- Monkey has the following features:
	- C-like syntax 
	- variable bindings 
		- let stmts can also be used to bind functions to names. Implicit return values are also possible, which means we can leave out return if we want to.
	- integers and booleans 
	- arithmetic expressions 
	- built-in functions 
	- first-class and higher order functions 
		- functions that take other functions as arguments. 
		- functions in monkey are just values, like strings or integers.
	- closures 
	- string data structure 
	- array data structure 
	- hash data structure 

- Binding Values to names in Vanara:
```js 
let age = 1;
let name = "Monkey";
let result = 10 * (20 /2);
```
- Also support arrays and hashes:
```js 
let myArray = [1,2,3,4,5];
```
- Hash , where values are associated with keys:
```js
let myHash = {
	"property1": hashValue1,
	"property2": hashValue2
};
```
- Accessing the elements in arrays and hashes , done using index expressions:
```js 
myArray[0];
```
- Like in JS, let stmts can also be used to bind functions to names.
```js
let addItem = fn(a,b) {
	return a+b;
}
```
- In Vanara, implicit return values are also possible (kinda like Rust), meaning we can leave out the return if we want to:
```js
let add = fn(a,b) { a+ b;}
```
- Eg of a more complex function in Vanara:
```js
let fibonacci = fn(x) {
if (x == 0) {
	0
} else {
	if(x==1) {
		1
	} else {
		fibonacci(x-1) + fibonacci(x-2)
	}
}
}
```
- Vanara also supports a special type of function, called as a higher order functions. These are functions that take other functions as arguments. ie. we can use functions as arguments in function calls. Functions in Vanara are just values, like integers or strings. That feature is called as "first class functions".
```js 
let twice = fn(f,x) {
	return f(f(x));
}

let addTwo = fn(x) {
	return x+ 2;
}

twice(addTwo,2);
```


### Features of the Interpreter:
- The interpreter will tokenize and parse Vanara source code in a REPL, building up an internal representation of the code called abstract syntax tree and then evaluate this tree. It will have a few major parts:
	- the lexer
	- the parser 
	- the Abstract Syntax Tree(AST)
	- the internal object system
	- the evaluator

