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

### Class Variables vs Instance Variables:
- Instance variables vary from object to object and are **declared in the constructor.**

```python
class Wall:
    def __init__(self):
        self.height = 10

south_wall = Wall()
south_wall.height = 20 # only updates this instance of a wall
print(south_wall.height)
# prints "20"

north_wall = Wall()
print(north_wall.height)
# prints "10"
```
- Class variables remain the same between instances of the same class and are **declared at the top level of a class definition**.

```python
class Wall:
    height = 10

south_wall = Wall()
print(south_wall.height)
# prints "10"

Wall.height = 20 # updates all instances of a Wall

print(south_wall.height)
# prints "20"
```


- In other languages these types of variables are often called [static variables](https://en.wikipedia.org/wiki/Static_variable).

- Variables, fields and properties
	- The terms instance and class variable, field, property and attribute are used interchangeably and usually refer to the same concept in languages that support some form of object-oriented programming. Here's a quick reference for some popular languages:

| Language   | Class variable | Instance variable |
| ---------- | -------------- | ----------------- |
| Python     | Class variable | Instance variable |
| Go         | Field          | Field             |
| JavaScript | Property       | Property          |
| C#         | Static field   | Field             |
| Java       | Static field   | Field             |

- Which should I use?
	- Generally speaking, _stay away from class variables_. Just like global variables, class variables are usually a bad idea because they make it hard to keep track of which parts of your program are making updates. However, it is important to understand how they work because you may see them out in the wild.

### Encapsulation:
- [Encapsulation](https://en.wikipedia.org/wiki/Encapsulation_(computer_programming)) is the practice of hiding complexity inside a ["black box"](https://en.wikipedia.org/wiki/Black_box) so that it's easier to focus on the problem at hand.
- The most basic example of encapsulation is a function. The caller of a function doesn't need to worry too much about what happens inside, they just need to understand the inputs and outputs.

```python
acceleration = calc_acceleration(initial_speed, final_speed, time)
```
- To use the `calc_acceleration` function, we don't need to think about every individual line of code inside the function. We just need to know that if we give it the inputs:
	- `initial_speed`
	- `final_speed`
	- `time`
- Then it will give us the correct `acceleration` as an output.
- By default, all properties and methods in a class are _public_. That means that you can access them with the `.` operator:

```python
wall.height = 10
print(wall.height)
# 10
```
- [Private](https://docs.python.org/3/tutorial/classes.html#tut-private) data members are how we encapsulate logic and data within a class. To make a property or method private, you just need to prefix it with two underscores.

```python
class Wall:
    def __init__(self, armor, magic_resistance):
        self.__armor = armor
        self.__magic_resistance = magic_resistance

    def get_defense(self):
        return self.__armor + self.__magic_resistance

front_wall = Wall(10, 20)

# This results in an error
print(front_wall.__armor)

# This works
print(front_wall.get_defense())
```
- Encapsulation is the practice of hiding code complexity inside a ["black box"](https://en.wikipedia.org/wiki/Black_box) so that other developers working with the code don't have to worry about it.
- To be clear, it does _not_ make the code more secure in a cryptographic or cyber-security sense. That's a point I was personally confused about when I was first learning about private and public class members.
- **Encapsulation is about organization, not security.**
- Encapsulation is like folders in an unlocked filing cabinet. They don't stop someone from peeking inside, but they do keep everything tidy and easy to find.
### Encapsulation in Python
- Python is a dynamic language, and that makes it difficult for the interpreter to enforce some of the safeguards that languages like [Go](https://go.dev/) do. That's why encapsulation in Python is achieved mostly by [convention](https://en.wikipedia.org/wiki/Coding_conventions) rather than by _force_.
- Prefixing methods and properties with a double underscore is a _strong_ suggestion to the users of your class that they shouldn't be touching that stuff. If a developer wants to break convention, [there are ways to get around](https://stackoverflow.com/questions/3385317/private-variables-and-methods-in-python) the double underscore rule.

```python
class Wall:
    def __init__(self, height):
        # the double underscore make this a private property
        # but it's not strictly enforced, there are hacks to get around it
        self.__height = height

    def get_height(self):
        return self.__height
```

### Abstraction:
- Abstraction helps us handle complexity by hiding unnecessary details. Sounds like encapsulation, right? They're so similar that it's almost not worth worrying about the difference...almost.
- Abstraction vs encapsulation
	- Abstraction is about _creating a simple interface for complex behavior._ It focuses on what's exposed.
	- Encapsulation is about _hiding internal state._ It focuses on tucking implementation details away so no one depends on them.
- Abstraction is more about reducing complexity, encapsulation is more about maintaining the integrity of system internals.
- Are we encapsulating or abstracting?
- Both. Almost always we are doing both. Here's an example of using the `random` library to generate a random number:

```python 
import random

attack_damage = random.randrange(5)
```
- Abstraction is about reducing complexity. Creating good abstractions is particularly crucial when you're developing libraries for other developers to use. For example, the built-in `pow` function in Python is an abstraction that hides the complexity of calculating exponents.

### OOP Thinking:
- lasses in object-oriented programming are all about grouping data and behavior _together_ in one place: an _object_. Object-oriented programmers tend to think about programming as a modeling problem. They think:
> "How can I write a `Human` class that holds the **data** and simulates the **behavior** of a real human?"
- To provide some contrast, functional programmers tend to think of their code as inputs and outputs, and how those inputs and outputs transition the world from one state to the next:
> "When a human takes a step, what's the new state of the game?"
- OOP isn't the only pattern for organizing code, but it's one of the more popular ones. If you understand multiple ways of thinking about code, you'll be a much better developer overall.