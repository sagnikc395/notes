# Definitions and the Environment 

- Any programming language that anyone uses has some notion of varibale binding that assigns a identifier to some value in the programming language.
- Core ideas about how varibales are issued in programming languages.
- Environment -> Variables and Bindings in scope at any given syntactic point within the program.
- Prelude -> built one operators and anything like +etc. what we think are built in operators.
- Racket also gives us bindings for macros.

## Two main forms to add things to Racket:
### Definitions:
- The form define is used to define variables.
- Define comes in 2 forms:
  - (define id expr) -> define varibale id as expr
  - (define (f a0 ...)body ...+)
    - define a function f with arguments a0,...
    - at least one body (typically only one)

### The Environment:
- The environment at some point in the prgoram includes the set of variables in scope -> accessible -> at that point.
- Every syntactic point has a potentially unique environment.
- Global variables are one top-level environment. always respecting the fact that only one top-level component may be required.
- Environments are specfic to an individual point and wont be the same at every point of the program.

### Environment Nest:
- Note that environments are heirarchical.
- Definitions inside a function do not escape the function.
- this relates to lexical scope which we will define soon.

- builtin functions like operators (+,-) etc. we can redefine them in our code in Racket and are not special.

### Let:
- Definitions with define are not expressions.
- (let ([var e]) e-body)
  - expression : evaluates e-body with var defined as e
  - can have more than one var
- let does not allow simulatnous bindings to see each other.
- like a parallel let.
Eg:
```scheme
(let ([x 2]
    [y x]) ;; bad 
    (+ x y))
```
### Let*:
- let* lets us define a sequence of variables.
- Think of this as a sequential let.
