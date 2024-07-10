---
---


## Lecture -0 Racket Basics 

### About the Course:
- Racket is the main programming language and using in this course.
- Wrap our mind around, minimal set of highly useful components.
- Racket features:
  - Dynamically Typed -> variables are untyped, values are typed.
  - Functional -> Racket emphasizes on functional style 
    - Compositional -> emphasizes black-box components 
    - Immutability -> required automatic memory management
  - Imperative -> allows data to be modified , in carefully considered cases, but doesnt emphasize "impure" code.

- Racket features not used in the course:
  - Object oriented -> racket has a powerful object system. Macros and Syntax expressions.
  - Language Oriented -> Racket is really a language toolkit -> easy to write DSL's for other programming languages. 
  - Homoiconic -> the same structure used to repersent data(lists) is also used to represent code.

- Every function in Racket is called using prefix notation , making them extremly uniform in syntax. We have a list of expression (f x y z) we can always identify the first as a function.
- when we define functions in Racket, we are also going to define them using prefix notation.
```scheme
(define (calculate-slope x0 y0 x1 y1)
  (/ (- y1 y0) (- x1 x0)))
```
- calls to used-defined functions are also in prefix mode.

- preferred style puts closing parens at end of blocks, instead of using a new line.

### Basic Types:
- Numeric Tower: Numeric Types gracefully degrade.
  - Eg: (* (/ 8 3) 2+1i) is 16/3+8/3i
  - Note that 2+1i is a literal value as is 2.3
- Strings and Characters ("foo" and #\a)
- Booleans(#t and #f) including logical operator(eg: or)
  - note that operators "short circuit" (|| , &&)
  - notion of truthy and falsiness.

- Symbols: are interned string 'foo , except a special property, if foo is a sumbol exists in meory, only one such exists in memory.
  - Implicit only one copy of each, unlike (say) strings.
  - Impact on space/memory usage. 
- #<void> value -> produced ((void))

- Predicate -> a single argument function in racket that returns either #t or #f.

  

