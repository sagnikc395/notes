---
title: Semigroup Intro
tags:
  - category-theory
  - fp
  - rust
date: 29/12/24
---
(ref: https://chshersh.com/blog/2024-07-30-pragmatic-category-theory-part-01.html)
### Why of Semigroup ? 
- Semigroup is an abstraction that supports quite a large number of diverse use cases.
	- Map Reduce 
	- CS Data Structures such as Segment Tree, Treap and Rope.
	- Optimal Multiplication and string concatenation algorithms
	- Blazing fast string builder 
	- Composable lexicographic comparison API
	- Set and Dictionary union 
	- Combining config files, CLI and environment arguments 
	- Composable validation 
	- Composable logging 
	- Builder pattern from OOP.
	- Sane JSON merging for structured logging.
### What is Semigroup actually ?
- Semigroup is a pair of a type and an operation of appending 2 values of these types to get a third value of the same type.
- In Category Theory notation: `A semigroup is a hom-set in a semicategory with a single object.`
- We can call this operation as append, add, multiply,combine,compose,merge etc.
- We can define the type in Rust as :(copied from claude)
```rust 
trait Semigroup {
    // The associated type 't' from the OCaml signature
    type T;
    
    // The append function that takes two values and combines them
    fn append(&self, other: &Self::T) -> Self::T;
}
/*
Note OCaml's module type becomes a Rust trait.
- OCaml's abstract type t becomes a associated type T.
- append function takes references in Rust to follow Rust's ownership rules.
- Rust uses self parameter explicitly.
- */

```
- We have a type t and a binary function append that takes 2 values of type t and returns another value of type t. When we implement this trait, a developer needs to specify a concrete type t and implement the append function for that.
- However note that not every append creates a Semigroup.This append operation must satisfy one requirement = associativity.
- ie.
- `append a ( append b c) = append (append a b) c`
- 