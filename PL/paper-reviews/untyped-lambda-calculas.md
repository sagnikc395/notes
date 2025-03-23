---
title: Untyped Lambda Calculas
tags:
  - lambda-calculas
  - plt
  - typescript
date: 9/2/25
---
### Introduction:
I have been recently been interested in a lot about Programming Languages and the mathematical theory and underpinnings behind them. The Lambda Calculas introduced by Alonzo Church in 1930's is one of the most fundamental paper in this domain and this is an attempt to understand programming languages from a more mathematical perspective. I have referenced [this paper](https://personal.utdallas.edu/~gupta/courses/apl/lambda.pdf) to understand the concepts for this post.

Historically, lambda calculas was developed in a way to formally define logically what is computable and as a way to explore the concepts of functions and their applications. For the sake of simplicity, and to get a good understanding of the fundamentals, I have only covered the "untyped" implementation of the lambda calculas, i.e the one which does not include a type system to restrict the kinds of values that functions can operate on, as this makes it very simple but also very powerful , as it can easily represent any computable function.

### Core Concepts:

#### 1. Lambda Terms:
The paper begins by defining the expressions called as lambda terms, which are defined as follows:
	1. Variables: Symbols like `x`, `y`, `z` representing inputs or values.
	2. Abstractions: Lambda abstraction $\lambda$x.M represents a function. where 
		1. `x` -> parameter of the function
		2. `M` -> body of the function.
	3. Application: A function application `M N` applies the function M to the argument N.
		1. ($\lambda x.x)y$ -> applies the identity function to y, resulting in y.
#### 2. Reduction Rules:
