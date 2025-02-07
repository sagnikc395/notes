---
title: Computational Type Theory
tags:
  - type-theory
  - plt
date: 7/2/25
---

- Type theory from a computational perspective.
- Papers:
    - Constructive Mathematics and Computer Programming(by Martin-Lof)
    - Consabel etal NuPRL System+Semnatics 

- Plan:
    - Develop type theory starting with computation.
    - Theory of truth -> what is true ?
    - only satisfactory truth is based on the theory of computation.
    - Contrast type theory with formalism ->
        - much less theory of truth , rather empahsizing more on formal proof and derivation.
        - Formalism is theory of (formal) proof.
    - Cubical Type Theory / Higher Dimensional Type Theory 
        - End of Week

### Biggest Idea :
- Start with a programming language. 
- what that means ->
    - start with a deterministic operational semantics.
    - Assume some idea of abstract syntax with binding + scope -> 
        - substitution for variables.
    - Means that I have forms of expression.
        - Bindings of forms of expression $ E $ 
    - Two judgement forms :
        E val means E is fully evaluated.
    - Transition :
        one step of simplification of E acc to a deterministic rule.
        $ E -> E_prime $ 
