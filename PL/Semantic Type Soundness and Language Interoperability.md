---
tags:
  - type-theory
  - pl-research
---
## Semantic Type Soundness
- One technique for proving one type system is sound.
- Technique is based on general technique called "Logical Relations".
	- super general technique and applies for a lot of problems.

### Logical Relations:
- proof method for proving a lot of programming language properties.
- Most famous is for proving the termination of the simply typed lambda calculas.
- Simply Typed Lambda Calculas:
	- A programming language which has only simple types in it, no recursive types in it and no doing loops in it and
- using this can prove the termination in it .
- Type Soundness:
- these two properties are interested in proving the property of a single well typed program.
- but logical relations are generalized to a single problem , but a relation of programs.
- Eg: Given two program expression E1 and E2 , are they interchangeable if we pass them thorugh a larger program. -> **program equivalence/ contextual equivalence**.
- Unary Properties:
	- Termination 
	- Type Soundness / Safety
- Binary Properties:
	- Program Equivalence
	- Representation Independence:
		- lets say we implement a stack interface using linked list and a array and we want to prove it that clients of this interface can't really prove the difference.
		- the representation of the data structure that we implement does not affect the representation.
	- Parametricity :
		- universal types / polymorphism.
		- lets say we have a function that adds element to the list, it can be abstract type and it can added to the list(generic).
		- holds for generics/polymorphism.
	- in security typed programming languages:
		- establish the property that high security data will never flow to low security observers.
		- have to talk to 2 programming interfaces to do it.
	- Another form of Binary Equivalence is when 2 terms is coming from two different languages and we get to define how are they correct using Logical Relations -> to prove the correctness of the compiler. 
	- Once we implement the compiler, show compiler correctness would basically be any source code that any source code is related to the output of the compiler in the logical representation.
	- very generic technique.

## how can logical relations be used to prove soundness of language interoperability ?
- indexed by source types but inhabited only by target terms of a compiler.
- essentially sketch out how we can 