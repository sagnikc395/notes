- Building a tree-walking simple interpreter. Building our own lexer, parser, our own tree representation and our own evaluator.

### About the Monkey Programming Language:
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

- The interpreter will tokenize and parse monkey source code in a REPL , building up an internal repr of the code called abstract syntax tree and evaluate this tree. It will have a few major parts:
	- the lexer 
	- the parser 
	- AST 
	- internal object system
	- the evaluator 

