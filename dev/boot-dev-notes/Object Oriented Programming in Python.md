---
title: Object Oriented Programming In Python
tags:
  - python
  - boot-dev
  - oop
  - basic-programming
date: 3/1/25
---
### OOP:
- [Object-Oriented Programming](https://en.wikipedia.org/wiki/Object-oriented_programming), or "OOP", is a pattern for writing clean and maintainable code. Not everyone _agrees_ that object-oriented principles are the best way to write code, but, to be a good engineer, you should at least understand them.
### Clean Code:
- Paradigms like [object-oriented programming](https://en.wikipedia.org/wiki/Object-oriented_programming) and [functional programming](https://en.wikipedia.org/wiki/Functional_programming) are all about making code easier to work with and understand as the feeble humans we are. Code that's easy for humans to understand is called "clean code".
- Clean Code does not:
	- Make your programs run faster
	- Make your programs function correctly
	- Only occur in object-oriented programming
- Clean Code does:
	- Make code easier to work with
	- Make it easier to find and fix bugs
	- Make the development process faster
	- Help us retain our sanity

### Dry Code:
- Another "rule of thumb" for writing maintainable code is "Don't Repeat Yourself" (DRY). It just means that, when possible, you should avoid writing the same code in multiple places. Repeating code can be bad because:
	- If you need to change it, you have to change it in multiple places
	- If you forget to change it in one place, you'll have a bug
	- It's more work to write it over and over again

### Classes:
- A [class](https://docs.python.org/3/tutorial/classes.html) is a special type of value in an object-oriented programming language like Python. It's similar to a dictionary in that it usually stores other types inside itself.
```python
# Defines a new class called "Soldier"
class Soldier:
    health = 5
    armor = 3
    damage = 2
```
- Just like a string, integer or float, a class is a _type_, but instead of being a built-in type, your classes are custom types that you define.
- An object is just an [instance](https://stackoverflow.com/questions/20461907/what-is-meaning-of-instance-in-programming) of a class type. For example:
```python
health = 50
# health is an instance of an integer type
aragorn = Soldier()
# aragorn is an instance of the Soldier type (class)
```
- "Classes" are custom new types that we define as the programmer. Each new instance of a class is an "object".
### Methods:
- you might be wondering _why_ classes are useful, they're like [dictionaries](https://docs.python.org/3/tutorial/datastructures.html#dictionaries)... but worse!
- One thing that makes classes cool is that we can define [methods](https://docs.python.org/3/tutorial/classes.html#method-objects) on them. A method is a function that's tied directly to a class and has access to all its properties.
- self:
	- Methods are nested within the `class` declaration. Their first parameter is always the instance of the class that the method is being called on. By convention, it's called ["self"](https://docs.python.org/3/glossary.html#term-method). Because `self` is a reference to the object, you can use it to read and update the properties of the object.
	- Notice that methods are called directly on an object using the dot operator.
```python
my_object.my_method()
```
- methods can return values:
	- n contrast, methods often don't return anything explicitly because they can mutate the properties of the object instead. That's exactly what we did in the last assignment.
	- However, they _can_ return values if you want! They're just functions with access to an object, after all.
### Methods vs Functions:
- A method has all the same properties as a function, but it is tied directly to a class and has access to all its properties.
- A method _automatically_ receives the object it was called on as its first parameter.
- A method can operate on data that is contained within the class. In other words, you won't always see all the "outputs" in the `return` statement because the method might just mutate the object's properties directly.
- Because functions are more explicit, some developers argue that [functional programming](https://blog.boot.dev/clean-code/benefits-of-functional-programming/) is better than object-oriented programming. In reality, neither paradigm is "better", and the best developers learn and understand both styles and use them as they see fit.

### Constructor:
- It's more practical to use a [constructor](https://en.wikipedia.org/wiki/Constructor_(object-oriented_programming)). In Python, if you name a method [`__init__`](https://docs.python.org/3/reference/datamodel.html#object.__init__), that's the constructor and it is called when a new object is created.
- So, with a constructor, the code would look like this:
```python
class Soldier:
    def __init__(self):
        self.name = "Legolas"
        self.armor = 2
        self.num_weapons = 2
```
- Now we can make the starting armor and number of weapons configurable with some parameters!
```python
class Soldier:
    def __init__(self, name, armor, num_weapons):
        self.name = name
        self.armor = armor
        self.num_weapons = num_weapons

soldier = Soldier("Legolas", 5, 10)
print(soldier.name)
# prints "Legolas"
print(soldier.armor)
# prints "5"
print(soldier.num_weapons)
# prints "10"
```

### Multiple Objects:
- So for our wall class, I can create three different "instances" of the class. Or, in other words, I can create three separate objects.

```python
wall_maria = Wall(1, 2, 3)
wall_rose = Wall(4, 5, 6)
wall_sina = Wall(9, 8, 7)
```

- Objects are an instance of a class.
