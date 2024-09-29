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


### Functions:
#### Function Definitions:
```ocaml 
let x = 42;;
```
- this expression in it , but is not itself an expression. Rather here it is a definition. Definitions bind values to nanes, here the value 42 is being bound to the name x.
- Definitions are not expressions, nor are expressions definitions -> they are distinct syntactic classes.
- Non recursive functions are defined as :
```ocaml 
let f x = ...
```
- recursive functions are defined as:
```ocaml
let rec f x = ...
```
- OCaml integers are not the "mathematical" integers but are limited to a fixed number of bits. 
	- Signed integers are at atleast 31 bits, but they could be wider.
	- In current implementations, OCaml integers are 63 bits.
	- Why 31/ 63 bits ? OCaml garbage collector needs to to distinguish between integers and pointers. The runtime repr of these therefore steals 1 bit of flag to whether a word is an integer or a pointer.
```ocaml 
let rec pow x y = if y = 0 then 1 else x * pow x (y-1)
```
- Ocaml compiler infers them for us automatically. Compiler solves this type inference problem algorithmically, but we can do it ourselves too.
	- Since the if expression can return 1 in the then branch, we know by the typing rule for if that the entire if expression has type int.
	- Since the if expression has type int, the function's return type must be int.
	- Since y is compared to 0 with the equality operator ,y, must be an int.
	- Since x is multiplied with another expression, using the * operator , x must be an int.

- Parentheses are mandatory when we write the type annotations for x and y. 
#### Anonymous Functions:
- Ocaml functions do not have to have names, they may be anonymous.
```ocaml 
let inc x = x + 1 
let inc. = fun x -> x + 1
```
- fun here is a keyword indicating an anonymous function, x is the argument and -> seperates the argument from the body.
- Anonymous functions are also called lambda expressions -> a term that comes from the lambda calculas -> mathematical model of computation in the same sense that Turing machines are a model of computation. In lambda calculas , fun x -> e would be written `\lambda x.e` . Lambda denotes an anonymous function.
- Often used to create anonymous functions and pass them as input to other functions.
#### Function Application:
```ocaml 
e0 e1 e2 .... en 
```
- First expression e0 is the function, and it is applied to arguments e1 through en.
- If we compare these evaluations rules to the rules for let expressions , we will notice that they both involve substitution. This is not an accident. So anywhere let x = e1 in e2 appears in a program, we could replace it with ( fun x -> e2) e1.
- They are syntactically different but semantically equivalent. In essence, let expressions are just syntactic sugar for anonymous function applications.

#### Pipeline:
- Built-in infix operator in OCaml for function application called the pipeline operator , written as | > .
- Values are sent through the pipeline from left to right.
```ocaml 

let square x = x * x 

(* ways to square it *)
square (inc 5);;
5 |> inc |> square;
```
- Latter uses the pipeline operator to send 5 through the inc function, then send the result of that through the square function.
- It is a idiomatic way of expressing the computation in OCaml. Former way is arguably not as elegant -> it involves writing extra parentheses and requires the reader's eyes to jump around -> eather than move linearly from left to right.
```ocaml 
5 |> inc |> square |> inc |> inc |> square;;
```
- e1 |> e2 is just another way to writing e2 e1, we dont need to state the semantics for |> , it's just the same as function application.
#### Polymorphic Functions:
```ocaml
let id x = x
```
- Identity function is the function that simply returns its input.
- 'a -> type variable , standing for a unknown type, just like a regular variable stands for an unknown value.
- Type variable always begins with a single quote.
- Commonly used type variables include 'a , 'b, 'c , which OCaml programmers typically pronounce in Greek: alpha, beta and gamma.
- Since we can apply id to many types of values -> it is a polymorphic functions -> it can be applied to many (poly) forms (morph).
- With manual type annotations -> possibel to give a more restrictive type to a polymorphic function than the type the compiler automatically infers.
```ocaml
let id_int (x: int): int = x;;
```
- another way of writing this:
```ocaml 
let id_int' : int -> int = <fun>;;
```
- Type of id_int specifies one aspect of its behaviour -> given an int as input, it promises to produce an int as output. 
- id also makes the same promise -> given an int as input , it too will return an int as output.
- Now id will also make many more promises -> eg: given a bool as input, it will return a bool as output. So by binding id to a more restrictive type int -> int , we have thrown away all those additional promises as irrelevant.
- Converse is not true -> if we needed a function of type 'a -> 'a but tried to use a function of type int -> int, we would be in trouble as soon as someone passed as input of another type, such as bool.
- To prevent the trouble , OCaml does something potentially surprising with the following code:
```ocaml 
let id' : 'a -> 'a = fun x -> x + 1 ;;
```
- id' is actually the increment functions , so OCaml will only use data + can safely manipulate are integers. OCaml therefore instantiates the type variable 'a to int -> thus preventing us from applying id' to non-integer.
- Another way to think about is in terms of application. By that we mean the very same notion of how a function is applied to arguments -> when evaluating the application id 5, the argument x is instantiated with value 5. Likewise the 'a in the type of id is being instantiated with type int at that application.
```ocaml 
let id_int' : int -> int = id 
```
- here we are instantiating the 'a in the type of id with the type int. Like there is no way to "unapply" a function -> eg: given 5 we can't compute backwards to id 5- we can't unapply that type instantiation and change int back to 'a.

#### Labelled and Optional Arguments:
- Type and name of a function usually gives us a pretty good idea of what the arguments should be.
- For functions with many arguments -> it can be useful to label them.
- Eg: function String.sub returns a substring of the given string. 
	- Can get the type of a function from utop by typing it.

- Ocaml supports labelled arguments to functions. We can declare this kind of function using the following syntax:
```ocaml 
let f -name: arg1 -name2: arg2 = arg1 + arg2 ;;
```
- Labels for arguments are often the same as the variable names for them. OCaml provides a shorthand for this case:
```ocaml 
let f -name1:name1 -name2:name2 = name1 + name2;;
let f -name1 -name2 = name1 + name2;;
```
- Used of labelled arguments is largely a matter of taste. They convey extra info, but they can also add cluster to types.
```ocaml
let f ?name1:(arg1=8) arg2 = arg1 + arg2 ;;
```

#### Partial Application:
```ocaml 
let addx x = fun y -> x + y;;
```
- here addx takes an integer x as input and returns a function of type int -> int that will add x to whatever is passed to it.
- here the type of addx is int -> int -> int. Here we can just apply it just to a single argument.
- This is called a partial application -> we partially applied the function add to one argument, even though we would normally think of it as a multi-argument function. This works because following 3 functions are syntactically different but semantically equivalent.
```ocaml
let add x y = x + y
let add x = fun y -> x + y 
let add = fun x -> (fun y -> y + x);;
```

#### Function Associativity:
- Every OCaml function takes exactly one argument -> i.e every function is currying.
```ocaml 
let f x1 x2 ... xn = e 
```
- is equivalent to:
```ocaml
let f = 
	fun x1 -> 
	(fun x2 -> 
	( ... 
		(fun xn -> e)...))
```
- Function types are right associative -> function takes a single argument and returns a new function that expects the remaining arguments.
- Function application however , is left associative, there are implicit parentheses around function applications, from left to right.

#### Operators as Functions:
- Adding parentheses around the + operator , we can make it as prefix operator.
```ocaml
( + ) 3 4 ;;
```
- Same technique works for any built-in operator.
- Normally spaces are unnecessary except for the multiplication , which must have spaces otherwise, it would be parsed as a comment.
- Can also our own operaters as:
```ocaml 
let ( ^^ ) x y = max x y;;
```
#### Tail Recursion:
- Call Stack has a limited size. size of stack is usually limited by the OS. So if the stack runs out of space, it becomes impossible to make another function call.
- In cases, where it does happe, there is a good reason for the OS to make the program stop, it might be in the process of eating up all the memory available on the entire computer, thus harming other programs running on the same computer.
- So the OS for safety's sake limits the call stack size.
```ocaml 
let rec count n = 
	if n = 0 then 0 else 1 + count(n-1);;
```
- rather after the recursive call count (n-1), there is computation remaining -> the computer still needs to add 1 to the result of that call.
- To optimize this, we need not do any additional computation after the recursive call. The trick is to create a helper function with an extra parameter.
```ocaml 
let rec count_aux n acc = 
	if n = 0 then acc else count_aux (n-1) (acc+1)
let count_tr n = count_aux n 0
```
- count_aux is almost the same as our original count, but it adds an extra parameter named acc, which is idiomatic and stands for "accumulator".
- The idea is that the value we want to return from the function is slowly, with each recursive call, being accumulated in it.
- "Remaining computation" -> the addition of 1 -> now happens before the recursive call not after.
- But the original base case of 0 still needs to exist in the code somewhere. And it does, as the original value of acc that is passed to count_aux. Now count_tr works as replacement for our original count.
- **A good compiler can notice, when a recursive call is in tail position, which is a technical way os saying "there is no more computation to be done after it returns".**
- A recursive call in tail position does not need a new stack frame. It can just reuse the existing stack frame.
	- nothing left to use in the existing stack frame!
	- So instead of wasting space by allocating another stack frame , the compiler "recycles" the space used by the previous frame.
- Tail call optimization can be applied in cases beyond recursive functions if the calling function's stack frame is suitably compatible with the callee. Tail-call optimization reduces the stack space requirements from linear to constant.
##### Importance of Tail Recursion:
- It is important that the compiler supports the optimization. Otherwise, the transformations we do to the code as programmer makes no difference. Most compilers do support it at least as a option, Java is an exception.

#### Recipe for Tail Recursion :
1. Change the function into a helper function. Add a extra argument: the acc -> the accumulator.
2. Write a new "main" version of the function that will call the helper. It will pass the original base case's return value as the initial value of the accumulator.
3. Change the helper function to return the accumulator in the base case.
4. Change the helper function's recursive case. It will now need to the extra work on the accumulator argument -> before the recursive call.

### Documentation:
- OCaml provides a tool called OCamlDoc that works a lot like Java's JavaDoc tool -> it extracts specially formatted comments from source code and renders them HTML,making it easy for programmers to read docs.

#### How to Document:
- double asterisk is what causes the comment to be recgonized as an OCamldoc comment.
- Square brackets around parts of the comment mean that those parts should be rendered HTML as type-writer font rather than the regular font.
- Ocamldoc like Javadoc supports docs tags like @author , @deprecated , @param , @return etc.

#### What to Document:
- follow concise and declaraitve documentataion.
- Comment starts with the sum , i.e example of the application of the function to an argument. The comment continues with the word 'is' thus declaratively describing the result of the application.
- That description uses the name of the argument, lst, to explain the result.
- There is no need to add tags to redundantly describe parameters or return values, as is often done with Javadoc.
- Another improvement for docs is to explicitly state what happens with empty lists.

#### Preconditions and Postconditions:
- requires clause above is the doc of random_int is a kind of precondition. It says that the client of the random_int function is responsible for guranteeing something about the value of bound.
- Similarly , the first sentence of that same doc is a kind of precondition. It gurantees something about the value returned by the function.
- Ocaml developers do not document the types of the function, because the compiler itself does the type checking to ensure that we never pass a value of the wrong type to a function.

### Printing:
- OCaml has a built-in printing functions for a built-in primitive types: print_chat,print_string,print_int,print_float.
- print_endline -> like print_string but with a newline.
### Unit:
- print_endline , print_string return a Unit type.
- There is only one value of this type, which is written () and is also pronounced "unit". So unit is like bool, except there is one fewer value of type unit than there is of bool.
- Unit is used when we need to take an argument or return a value, but there is no interesting value to pass or return.

### Semicolon:
- 
