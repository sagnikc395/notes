---
title: Parser Combinators
tags:
  - parser-combinators
  - pl-research
  - ocaml
---
## why and how of parser combinators 
- angstorm -> parsec for ocaml , parser combinators library to rewrite parsing in OCaml.

### Monadic Parser Combinators:
- by Graham Hutton. -> more of a report.
- Parser takes a string of input and creates a data structure out of it -> makes sense of plaintext.
- Used pretty much everywhere Eg: HTML parser, CSS parser etc.
- All compilers will have a parser, by respect out of what they do. Most commerical applications have a parser built into it somewhere.
- OCaml doesnt have typeclasses.(?)
- Can still build a lot of things and build on top of it.
- Parser combinators is a library that will give us tools to help us build larger parsers incremently.
- the whole idea is to parse some input and leave rest of the thing to be parsed.

### Monad Interface:
- Operation called pure of some type and creates a parser that will always return the value and does not touch the input.
- Unit methods 
- And secondly need a way to combine them.
- Then it will use bind operator -> take 2 parsers and then combine them against each other.
- Bind -> take a parser as a input and then compose other on top of each other. It will give another input and a parser and returns the current character.
- To add more combinators and monadic helpers.

### Lifting in Haskell for parsers.

### parsers operating under a parsing context 


