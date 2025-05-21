---
title: Why Lean and why proof oriented programming langs ?
tags:
  - lean4
  - functional-programming
  - dependent-type-theory
date: 12/5/25
---
### why lean ?
- Lean is an interactive theorm prover , based on dependent type theory. It unites the world of programs and proofs : Lean is also a programming language.
- Lean takes its dual nature seriously -> designed to be suitable for use as a general purpose programming language -> infact Lean compiler is implemented in itself.

- Lean is a strict pure functional language with dependent types. A large part of learning to program with Lean consists of learning how each of these attributes affects the way programs are written, and how to think like a functional programmer.

- Strictness -> that function calls in Lean work similarly to the way they do in most languages i.e arguments are fully computed before the function's body begins running.

- Purity -> Lean programs cannot have side effects such as modifying locations in memory, sending emails or deleting files without the program's type saying so. Lean is a functional language in the sense that functions are first-class values like any other and that the execution model is inspired by the evaluation of mathematical expressions.

- Lean is a functional language in the sense that functions are first-class values like any other and that the execution model is inspired by the evaluation of mathematical expressions. 

- Dependent types , which are the most unusual feature of Lean, make types into a first-class part of the language , allowing types to contain programs and programs to compute types.


### Lean Env:
- elan -> manages the Lean compiler toolchains -> like rustup
- lake -> builds Lean packages and their dependencies, similarly to cargo, make or Gradle.
- lean type checks and compiles individual Lean files as well as providing information to programmer tools about files that are currently being wtitten. Normally, lean is invoked by other tools rather than directly by users.
- Plugins for editors, like VScode or Emacs that communicate with lean and present its information conviniently.




