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
- We can bind values to names with a let definition:
```ocaml
let x = 42
```
- Here:
	- a value was bound to a name,hence the val keyword.
	- x is the name to which the value was bound.
	- int is the type of the value
	- 42 is the value.

### Functions:
- A function can be defined at the toplevel using syntax:
```ocaml 
let increment x = x + 1
```
- Here:
	- increment : identifier to which the value was bound 
	- int -> int : type of the value. This is the type of function that takes an int as input and produce an int as output. Think of the arrow -> as a kind of visual metaphor for the transformation of one value into another value -> which is what functions do.
	- Value is a function, which the toplevel choses not to print. Instead the toplevel prints `<fun>`, which is just a placeholder.
- Can call the syntax as :
```ocaml
increment 0;; 
increment(21);;
increment (increment 5);;
```
- In OCaml, the vocabulary is that we "apply" the function rather than "call" it.
- OCaml is flexible about whether we write the parentheses or not and whether we write whitespace or not.
- Preferred style , though, is usually to omit parentheses when they are not needed.

### Loading Code in the Toplevel:
- Toplevel will also accept directives that are not OCaml code but rather tell the toplevel itself to do something. 
- All directives begin with the # character.
- `#use` loads all the code from a file into the toplevel, just as if we had typed the code from the file into the toplevel.
```ocaml
# #use "mycode.ml";; 
let inc x = x + 1;;
```

### Workflow in Toplevel:
- Best workflow when using toplevel with code stored:
	- Edit the code in the file 
	- Load the code in the toplevel with #use 
	- Interactively test the code.
	- Exit the toplevel.


### Compiling OCaml Programs:
- main method in ocaml:
```ocaml
let _ = print_endline "Hello world!"
```
- ```let _ =``` above means that we dont care to give a name to code on the right hand side of the =. We can then compile the code using ocamlc.
- Compiler is called ocamlc. -o flag says to name the output the executable name.
- Executable contains simplified OCaml bytecode. In addition, other files are produced, hello.cmi and hello.cmo. 
- Unlike C/Java, OCaml programs do not need to have a special function names main that is invoked to start the program. Usual idiom is just to have the very last definition in a file serve as the main function that kicks off whatever the computation is to be done.
### Dune:
- build systems to automatically find and link in libraries.
- Legacy build system like ocamlbuild exists and a newer build system called Dune.
- Dune project is a directory that contain OCaml code that we want to compile. The root of a project is the highest directory in its hierarchy. A project might rely on external packages providing additional code that is already compiled. Usually , packages are installed with OPAM -> OCaml Package Manager.
- Each directory in our project can contain a file called dune. That files describes to Dune how we want the code in that directory and subdirectories to be compiled.
- Dune uses Lisp syntax to show nested data that form a tree,much like HTML tags do.

### Creating Dune Project Manually:
```scheme 
(executable 
	(name hello))
```
- this declares an executable (a program that can be executed) whose main file is hello.ml.
- Also creates a file called dune-project and add the dune config 
```scheme 
(lang dune 3.4)
```
- This will tell Dune to use Dune v3.4. This project file is needed in the root directory of every source tree that we want to compile with Dune. In general, we will have a Dune file in every subdirectory of the source tree but also one dune-project file at the root.
```sh 
dune build hello.exe
```
- .exe is the universal extension, not just Windows. This causes Dune to build a native executable rather than a bytecode execuable.

#### _build: 
- Dune will create this directory and compile our program inside it. That's one benefit of the build system over directly running the compiler: instead of polluting our source directory with a bunch of generated files, they have got cleanly created in a seperated directory.
- Inside ```_build``` there are many files that get created by Dune.
- Run dune clean to remove the build artifacts.

### Creating a Dune Project Automatically:
- Traverse in the directory where we want to store our work, and select the name for our project, run:
```shell 
$ dune init project calculator
$ cd calculator
$ code .
```
- We should have code open and see the files that Dune automatically generated for our project.
- From the termianl we can run diretly:
```sh 
$ dune exec bin/main.exe
``` 

### Running Dune Continousuly:
- When we run dune build, it compiles our project once. We might want to have our code compiled automatically every time we save our file, to do that we can do enable the ```--watch``` flag when we do dune build.
- Dune will responsd that is waiting for fs changes. That means Dune is running continuously and rebuilding our project every time we save a file in code.

### Expressions:
- Like programs in imperative languages are primarily built out of commands , program in functional languages are primarily build out of expressions.
	- Eg: 2+2, increment 21 
- Primary task of computation in a functional language is to evaluate an expression to a value. A value is an expression for which there is no computation remaining to be performant.
- So all values are expressions, but not all expressions are values.
	- Eg: 2, true, "yay!"
- Sometimes an expression might fail to evaluate to a value, there are 2 reasons that might happen:
	- Evaluation of the expression raises an exception.
	- Evaluation of the expression never terminates.(eg: it enters an "infinite loop")

### Primitive Types and Values:
- The primtive types are the built in and most types: integers,floating-point numbers,characters, strings and booleans.
- They will be recognizable as similar to primitive types from other programming languges.
- **int** -> Integers. OCaml integers are written as usual 1,2 etc. The usual operators are available: +,-,*,/ , mod.
	- OCaml integers range from -2^62 to 2^62 -1 on 64 bit processeors.They are implemeneted with 64 bit machine words, i.e the size of a register on 64bit processor.
	- 1 bit is "stolen" by the OCaml implementation, leading to a 63 bit repr. That bit is used at run time to distinguish integers from pointers.
	- For application, that need true 64bit integers, there is the Int64 module. 
	- For applications that need arbitary precision integers, there is a Zarith library, but for most purposes, the built-in int type suffices and offers the best performance.
- **float** -> Float . OCaml floats are IEE754 double floating point numbers. Syntactically, they must always contain a dot 3.14,3.0 or even 3. The last is float.
	- OCaml does not support operator overloading, Arithmatic operations on floats are written with a dot after them.Eg: `*.`
	for floating point multiplication.
	- OCaml will not automatically convert between int and float. If we want to convert, there are 2 bulit-in functions for that purpose -> int_of_float and float_of_int.
- **bool** -> Boolean . written as true and false. short circuit conjunction && and disjunction || operators are available.
- **char** -> Characters -> Written with single quotes, such as 'a','b' and 'c'. They are repr as bytes -> 8-bit integers. First half of the cahracters in that range are the standard ASCII characters. We can convert characters to and from integers with char_of_int and int_of_char.
- **string** -> Strings . Strings are sequences of characters. They are written with double quotes, such as "abc". String concatenation operator is ^.
	- OOP languages often provide an override method for converting objects to strings. Most OCaml values are not objects, so another means is required to convert strings.
		- for the primitive types , there are built-in funcs:
			- string_of_int,
			- string_of_float,
			- string_of_bool 
			- String.make -> no string_of_char
	- Similarly there exists inverse operator for the converse:
		- int_of_string
		- float_of_string
		- bool_of_string 
	- no char_of_string, but string character can be accessed using a 0-based index. Indexing operator is written with a dot and square brackets.
### More Operators:
- There are 2 equality operators in OCaml, = ,== with corresponding inequality operators <> and !=.
- Operators = and <> examine structural equality whereas == and != examine physical equality.

### Assertions:
- assert e evaluates e. If result is true , nothing more happens and the entire expression evaluates to a special value called unit. 
- The unit value is written () and its type is unit. 
- But if the result is false, an exception is raised.
```ocaml
let () = assert (f input1 = output1)
let () = assert (f input2 = output2)
let () = assert (f input3 = output3)
```

### If Expressions:
- if e1 then e2 else e3 evaluates to e2 if e1 evals to true and to e3 otherwise. We call e1 the guard of the if expression.
- Unlike the if-then-else statements , we may have used in imperative languages, if-then-else expressions in OCaml are just like any other expression -> they can be put anywhere an expression can go. This makes them similar to the ternary operator ?: , that we might have used in other languages.
```ocaml
if e1 then e2 
else if e3 then e4 
... 
else en
```
- e is an exmaple of a syntactic variable aka metavariable, which is not actually a variable in the OCaml language itself, but instead a name for a certain syntactic construct.
- Number after the letter e are being used to distinguish the 3 different occurneces of it.
### let expressions:
- let can also be used as an expression.
```ocaml
let x = 42 in x + 1 ;
```
- here we are binding a value to the name x then using that binding inside another expression, x+1. 
- We call this use of let as an let expression. Since it is an expression, it evaluates to a value.
- Different than definitions, which themselves do not evaluate to any value.
- Syntactically, a let definition is not permitted on the left-hand side of the + operator,because a value is needed there, and definities do not evaluate to values. On the other hand, a let expression would work fine:
```ocaml
(let x = 42 in x) + 1
```
- They are like let expression where we just haven't provided the body expression yet. Implicitly, that body expression is whatever else we type in the future.
```ocaml
let a = "big" in 
let b = "red" in 
let c = a ^ b in 
...
```
```ocaml 
let x = e1 in e2
```
- As usual, x is an identifer. These identifiers must begin with lower-case , not upper , and idiomatically are written with snake_case not camelCase.
- we call e1 , the binding expression, because it's what's being bound to x and we call e2 the body expression, because that's body of code in which the binding will be in scope.
- We use the parentheses above just for clarity. As usual, the compiler's type inference determines what the type of the variable is, or the programmer could explicitly annotate it with this syntax:
```ocaml
let x: t = e1 in e2
```
### Scope:
- let bindings are in effect only in the block of code in which they occur. This is exactly what we have used to form nearly any modern programming language.
- Scope of a variable is where its name is meaningful. Variable y is in scope only inside of the let expression that binds it above.
- Also possible to have overlapping bindings of the same name.
```ocaml
let x = 5 in ((
let x = 6 in x
) + x);;
```
- a new binding of a variable shadows any old binding of the variable name. Metaphorically, it's as if the new binding temporarily casts a shadow over the old binding. But eventually the old binding could reappear as the shadow receds.
- This is also called as shadowing. It is not mutable assignemnt.
```ocaml
let x = 5 in (( let x = 6 in x) + x);;
let x = 5 in ( x + (let x = 6 in x));;
```
- Since every let definition in the toplevel is effectively a nested let expression. So the above is effectively the following:
```ocaml
let x = 42 in 
	let x = 22 in 
	 ... (* whatever else is typed in toplevel *)
```
- Right way to think about this is that the second let binds an entirely new variable that just happends to have the same name as the first let.
- Each let definition binds an entirely new variable. If that new variable happens to have the same name as an old variable,the new variable temporarily shadows the old one. But the old variable is still around, and its value is immutable: it never,ever changes. So even though let expressions might superficially look like assignment statements from imperative languages.

### Type Annotations:
- OCaml automatically infers the type of every expression, with no need for the programmer to write it manually.
- Nonetheless, it can sometimes be useful to manually specify the desired type of an expression. A type annotation does that.
- Type annotations are not type casts, such as might be found in C/Java. They do not indicate a conversion from one type to antoher. Rather they indicate a check that the expression really does have the given type.
