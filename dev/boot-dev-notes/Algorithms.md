---
title: Algorithms
date: 9/1/25
tags:
  - basic-programming
  - algorithms
  - boot-dev
---

### Goals of Algorithms:
- **Learn to think algorithmically**. Break problems down into easier to solve parts.
-  **Learn about performance optimization**. Make your code run faster and more efficiently, even with more data.
-  **Practice solving hard problems**. There's no way around it, if you want to be a great developer, you need to solve hard problems.


### Find Minimum:
- An "algorithm" is just a set of instructions that can be carried out to solve a problem.
- People use algorithms all the time without even realizing it. Practically every function you write in code is an algorithm (well, kinda), even if it's a simple one.
```python 
def find_minimum(nums):
    if len(nums)==0:
        return None
    min = float("inf")
    for num in nums:
        if num < min:
            min = num 
    return min
```

### What is Algorithm:
- an [algorithm](https://en.wikipedia.org/wiki/Algorithm) is a finite sequence of well-defined, computer-implementable instructions. In short, an algorithm is:
	- **Defined**: there is a specific sequence of steps that performs a task
	- **Unambiguous**: there is a "correct" and "incorrect" interpretation of the steps
	- **Implementable**: it can be executed using software and hardware
- Algorithms are usually written in ["pseudocode"](https://en.wikipedia.org/wiki/Pseudocode) (pronounced "sue-dough-code") because an algorithm is a higher-level description of a solution to a problem. An algorithm doesn't care if it's implemented in Python, Go, TypeScript, or (gasp) Java. Pseudocode is just plain English that describes the steps of the algorithm.
- Here's some pseudocode for a mystery algorithm:
	1. Start with an original string called `S` and a new empty string called `R`.
	2. Loop through `S` from its last character to its first character, and for each one, add it to the end of `R`.
	3. Once you’ve processed all the characters, return `R`.

- Simple Algorithms:
```python 
import functools 
def sum(nums):
    return functools.reduce(lambda item,acc: item+acc,nums,0)
```
### Exponents:
- An [exponent](https://en.wikipedia.org/wiki/Exponentiation) indicates how many times a number is to be multiplied by itself.

- For example:
	- 53 = `5 * 5 * 5` = `125`
	- Sometimes exponents are also written using the caret symbol (`^`):
- `5^3` = 125
- The `**` operator calculates an exponent in Python. (Why not the `^` operator? Blame [Fortran](https://softwareengineering.stackexchange.com/a/331392).)

```python
square = 2 ** 2
# square = 4

cube = 2 ** 3
# cube = 8
```
- Exponents grow very large [**very quickly**](https://en.wikipedia.org/wiki/Wheat_and_chessboard_problem)
- 