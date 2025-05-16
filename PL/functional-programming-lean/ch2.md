---
title: Evaluating Expressions
tags:
  - lean4
  - dependent-type-theory
date: 12/5/25
---
- How does evaluation work in Lean ?
	- Evaluation is the process of finding the value of an expression, just as one does in arithmatic.
	- In Lean, programs are first and foremost expressions, and the primary way to think about computation is as evaluating expressions to find their values.
- Programs have access to mutable memory , so the value referred to by a variable can change over time. In addition to a mutable state, programs may have other side effects, like deleting files, making outgoing network connections, throwing or catching exceptions, and reading data from a database.
	- Side effects is effectively a catch all term for describing things that may happen in a program that don't follow the model of evaluating mathematical expressions.
#### How is Lean like maths
- Programs work the same way as mathematical expressions. Once given a value, variables cannot be reassigned. Evaluating an expression cannot have side effects.
- If two expressions have the same value , then replacing one with the other will not cause the program to compute a different result.
- While lean can and will write to the console, but performing I/o is not a core part of the experience of using Lean the same way.

#### eval:
- to ask lean to evaluate an expressions , write `#eval` before it in our editor, which will then report the result back. Typically, the result is found by putting the cursor or the mouse pointer over `#eval` 
- While both ordinary mathematical notation and the majority of programming langs use parentheses for application of a function to its arguments, Lean simply writes the function next to its arguments. Function application is one of the most common operations.
- Just as the order of operations rules for arithmatic demand parentheses in the expression, parentheses are also necessary when a function's argument is to be computed via another function call -> 
	- as then the second String.append would be interpreted as an argument to the first rather than as a function being passed "oak " and "tree" as arguments.
- Imperative languages have 2 kinds of conditionals : a conditional statements that determines which instructions to carry out based on a Boolean value and a conditional expression that determines which of the 2 expressions to evaluate based on a Boolean value.
	- Since Lean is a expression-oriented functional language, there are no conditional statements, only conditional expressions. Written using if, then and else.

#### potential errors:
- Asking lean to evaluate a function application that is missing an argument will lead to an error message.
```lean
#eval String.append "it is "
```
- this will give error as Lean functions that are applied to only some of their arguments return new functions that are waiting for the rest of the arguments. Lean cannot display functions to users, and thus returns an error when asked to do so.


