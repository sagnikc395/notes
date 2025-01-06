---
title: Functional Programming In Python
tags:
  - functional-programming
  - python
---

### what is functional programming ?
- Functional programming is a style (or "paradigm" if you're pretentious) of programming where we compose functions instead of mutating state (updating the value of variables).

- [Functional programming](https://en.wikipedia.org/wiki/Functional_programming) is more about declaring _what_ you want to happen, rather than _how_ you want it to happen.
- [Imperative](https://en.wikipedia.org/wiki/Imperative_programming) (or procedural) programming declares both the _what_ and the _how_.

- **Example of imperative code:**

```python
car = create_car()
car.add_gas(10)
car.clean_windows()
```
- **Example of functional code:**

```python
return clean_windows(add_gas(create_car()))
```
- In the functional example, we never change the value of the `car` variable, we just compose functions that return new values, with the outermost function, `clean_windows` in this case, returning the final result.
### Python is not the best for functional programming:
- Python is _not_ the best language for functional programming. Reasons include:

1. No [static typing](https://developer.mozilla.org/en-US/docs/Glossary/Static_typing).
2. Everything is [mutable](https://en.wikipedia.org/wiki/Immutable_object).
3. No [tail call optimization](https://exploringjs.com/es6/ch_tail-calls.html).
4. [Side effects](https://en.wikipedia.org/wiki/Side_effect_(computer_science)) are common.
5. Imperative and OOP styles abound in popular libraries.
6. [Purity](https://en.wikipedia.org/wiki/Pure_function) is not enforced (and sometimes not even encouraged).
7. [Sum Types](https://en.wikipedia.org/wiki/Algebraic_data_type) are hard to define.
8. [Pattern matching](https://en.wikipedia.org/wiki/Pattern_matching) is weak at best.

So seriously, why are we using Python?
- cause we already know it 

### Immutability:
- In FP, we strive to make data _[immutable](https://en.wikipedia.org/wiki/Immutable_object)_. Once a value is created, it cannot be changed. _Mutable_ data, on the other hand, can be changed after it's created.
- Why ?
	- Immutable data is easier to think about and work with. When 10 different functions have access to the same variable, and you're debugging a problem with that variable, you have to consider the possibility that any of those functions could have changed the value.
	- When a variable is immutable, you can be sure that it hasn't changed since it was created. It's a helluva lot easier to work with.
- _Generally speaking, immutability means fewer bugs and more maintainable code._
-  Tuples vs Lists
	- Tuples and lists are both ordered collections of values, but tuples are _immutable_ and lists are _mutable_.
- You can append to a list, but you can _not_ append to a tuple. You can create a _new copy_ of a tuple using values from an existing tuple, but you can't change the existing tuple.
- Lists are mutable
```python
ages = [16, 21, 30]
# 'ages' is being changed in place
ages.append(80)
# [16, 21, 30, 80]
```
-  Tuples are immutable
```python
ages = (16, 21, 30)
more_ages = (80,) # note the comma! It's required for a single-element tuple
# 'all_ages' is a brand new tuple
all_ages = ages + more_ages
# (16, 21, 30, 80)
```

- Functional programming aims to be _declarative_. We prefer to declare _what_ we want the computer to do, rather than muck around with the details of _how_ to do it.
- Declarative Programming:
	- It does _not_ execute line-by-line like an imperative language. Instead, it simply declares the desired style, and it's up to a web browser to figure out how to apply and display it.(CSS)
- Unlike functional programming (and CSS), a lot of code is _imperative_. We write out the exact step-by-step implementation details. This Python script draws a red button on a screen using the [Tkinter](https://docs.python.org/3/library/tkinter.html) library:

```python
from tkinter import * # first, import the library
master = Tk() # create a window
master.geometry("200x100") # set the window size
button = Button(master, text="Submit", fg="red").pack() # create a button
master.mainloop() # start the event loop
```
### It's just math:
- Functional programming tends to be popular amongst developers with a strong mathematical background. After all, a math equation isn't procedural: it's declarative. Take the following math equation:
```
	avg = Σx/N
```
- To put this calculation in plain English:

	1. `Σ` is just the Greek letter [Sigma](https://en.wikipedia.org/wiki/Sigma), and it represents "the [sum](https://en.wikipedia.org/wiki/Summation) of a collection".
	2. `x` is the collection of numbers we're averaging.
	3. `N` is the number of elements in the collection.
	4. `avg` is equal to the sum of all the numbers in collection "x" divided by the number of elements in collection "x".

- So, the equation really just says that `avg` is the average of all the numbers in collection "x". This math equation is a _declarative_ way of writing "calculate the average of a list of numbers". Here's some _imperative Python code_ that does the same thing:
```python 
def get_average(nums):
    total = 0
    for num in nums:
        total += num
    return total / len(nums)
```
- with functional programming, we would write code that's _a bit more_ declarative:

```python
def get_average(nums):
    return sum(nums) / len(nums)
```
### Classes vs Functions:
- I run into new developers who, after learning about classes, want to use them _everywhere_. They assume that because they learned about functions first, functions are somehow inferior.
- **If you're unsure, default to functions.** I find myself reaching for classes when I need something long-lived and stateful that would be easier to model if I could share behavior _and data structure_ via inheritance. This is often the case for:
	- Video games
	- Simulations
	- GUIs
- The difference is:
> **Classes** encourage you to think about the world as a hierarchical collection of objects. Objects bundle behavior, data, and state together in a way that draws boundaries between instances of things, like chess pieces on a board.

> **Functions** encourage you to think about the world as a series of data transformations. Functions take data as input and return a transformed output. For example, a function might take the entire state of a chess board and a move as inputs, and return the new state of the board as output.

### Debugging FP:
- 