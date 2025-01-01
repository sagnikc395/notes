---
title: Python from Scratch
tags:
  - basic-programming
  - python
  - boot-dev
date: 28/12/24
---
### Console:
- "console" is a panel that displays important messages, like errors or the text output of a program. If we want to see what's happening in our code, we need to print it to the console by using the `print()` function.
### What is Code:
- What is Code? 
	- Code is a just a series of instructions for a computer to follow one after another. Programs can have a lot of instructions.
	- Code runs in order, starting at the top of the program.

### Syntax:
- Syntax is jargon for valid code that the computer can understand. 
- The rules for how expressions and statements should be structured in languge can also be called as syntax.
- Syntax errors aren't the only kind of problems that you can run into when coding:
	- - **A bug in your logic**. Your code is _valid_, and will _run_, but it does something unexpected.
	- **It's too slow**. Your code is _valid_ and does _what's expected_, but it does it slowly

### Variables:
- [Variables](https://www.cs.utah.edu/~germain/PPS/Topics/variables.html) are how we _store_ data as our program runs.
- A "variable" is just a name that we give to a value. For example, we can make a new variable named `my_height` and set its value to `100`:
```py
my_height = 100
```
- Or we can define a variable called `my_name` and set it to the text string `"Lane"`:
```py
my_name = "Lane"
```
- Once we have a variable, we can access its value by using its name.
- Variables are called "variables" because they can hold any value and that value can change (it varies).
- Negative numbers in Python work the way you probably expect. Just add a minus sign.
- Python has built-in support for exponents - something most languages require a `math` library for.
- Plus Equals -> Python makes reassignment easy when doing math. In JavaScript or Go, you might be familiar with the `++` syntax for incrementing a number variable by 1. In Python, we use the `+=` [in-place operator](https://docs.python.org/3/library/operator.html#in-place-operators) instead.
- As we covered earlier, a `float` is a positive or negative number **with a fractional part**.
- You can add the letter `e` or `E` followed by a positive or negative integer to specify that you're using [scientific notation](https://en.wikipedia.org/wiki/Scientific_notation).

```python
print(16e3)
# Prints 16000.0

print(7.1e-2)
# Prints 0.071
```

- Python also allows you to represent large numbers in the decimal format using underscores as the [delimiter](https://en.wikipedia.org/wiki/Decimal_separator#Digit_grouping) instead of commas to make it easier to read.

```python
num = 16_000
print(num)
# Prints 16000

num = 16_000_000
print(num)
# Prints 16000000
```
- Logical operators deal with [boolean values](https://en.wikipedia.org/wiki/Boolean_data_type), `True` and `False`.
- The logical `and` operator requires that _both_ inputs are `True` to return `True`. The logical `or` operator only requires that _at least one_ input is `True` to return `True`.
- The `not` operator reverses the result. It returns `False` if the input was `True` and vice-versa.
- [Binary numbers](https://en.wikipedia.org/wiki/Binary_number) are just "base 2" numbers. They work the same way as "normal" base 10 numbers, but with two symbols instead of ten.
- Each `1` in a binary number represents an ever-greater multiple of 2. In a 4-digit number, that means you have the eights place, the fours place, the twos place, and the ones place. Similar to how in decimal you would have the thousands place, the hundreds place, the tens place, and the ones place.
- We can write an integer in Python using binary syntax using the `0b` prefix.
- Bitwise operators are similar to logical operators, but instead of operating on boolean values, they apply the same logic to all the bits in a value by column.
- A `1` in binary is the same as `True`, while `0` is `False`. So really a bitwise operation is just a bunch of logical operations that are completed in tandem by column.
- Ampersand `&` is the bitwise "and" operator in Python. "And" is the _name_ of the bitwise operation, while ampersand `&` is the _symbol_ for that operation.
- As you may have guessed, the bitwise "or" operator is similar to the bitwise "and" operator in that it works on binary rather than boolean values. However, the bitwise "or" operator "or"s the bits together.
- When coding it's necessary to be able to compare two values. `Boolean logic` is the name for these kinds of comparison operations that always result in `True` or `False`.
- The operators:
	- `<` "less than"
	- `>` "greater than"
	- `<=` "less than or equal to"
	- `>=` "greater than or equal to"
	- `==` "equal to"
	- `!=` "not equal to"
- Here are some basic rules with if/else blocks.
	- You can't have an `elif` or an `else` without an `if`
	- You _can_ have an `else` without an `elif`

### Comments:
- Comments don't do... anything. They are _ignored_ by the Python interpreter. That said, they're good for what the name implies: adding comments to your code in plain English (or whatever language you speak).
- You can use triple quotes to start and end multi-line comments as well.This is useful if you don't want to add the `#` to the start of each line when writing paragraphs of comments.
- Variable names can _not_ have spaces, they're continuous strings of characters.
	- The creator of the Python language himself, [Guido van Rossum](https://en.wikipedia.org/wiki/Guido_van_Rossum), [implores us](https://peps.python.org/pep-0008/#function-and-variable-names) to use `snake_case` for variable names. What _is_ snake case? It's just a style for writing variable names. 
- |Name|Code|Language(s) that recommend it|
|---|---|---|
|Snake Case|`my_hero_health`|Python, Ruby, Rust|
|Camel Case|`myHeroHealth`|JavaScript, Java|
|Pascal Case|`MyHeroHealth`|C#, C++|
|No Casing|`myherohealth`|No one: don't do this|

### Variable Types:
- Python has several basic [data types](https://en.wikipedia.org/wiki/Data_type).
- **Strings**
	- In programming snippets of text are called "[strings](https://docs.python.org/3/library/stdtypes.html#textseq)". They're lists of characters _strung_ together. We create strings by wrapping the text in single quotes or double quotes. That said, **double quotes are preferred**.
- **Numbers**:
	- Numbers are _not_ surrounded by quotes when they're declared.
	- **An [integer](https://docs.python.org/3/c-api/long.html) is a number without a decimal part**:
	- **A [float](https://docs.python.org/3/library/functions.html#float) is a number with a decimal part**:
- **Booleans**:
	- A ["Boolean"](https://docs.python.org/3/c-api/bool.html#boolean-objects) (or "bool") is a type that can only have one of two values: `True` or `False`. As you may have heard, computers really only use 1's and 0's. These 1's and 0's are just `True/False` boolean values.
### f-strings:
- In Python we can create strings that contain dynamic values with the [f-string](https://docs.python.org/3/tutorial/inputoutput.html#formatted-string-literals) syntax.
	- - Opening quotes must be preceded by an `f`.
- Variables within curly brackets have their values "interpolated" (injected) into the string.
- It's just a string with a special syntax.
### NoneType Variable:
- Not all variables have a value. We can make an "empty" variable by setting it to [`None`](https://docs.python.org/3/library/constants.html#None). `None` is a special value in Python that represents the absence of a value. It is _not_ the same as zero, False, or an empty string.
- [NoneType](https://docs.python.org/3/library/types.html#types.NoneType) is _not_ the same as a string with a value of "None".
- One usecase is to represent that a value hasn't been determined yet, for example, an uncaptured input.
### Dynamic Typing:
- Python is [dynamically typed](https://en.wikipedia.org/wiki/Type_system#Static_and_dynamic_type_checking_in_practice), which means a variable can store any type, and that type can _change_.
- In almost all circumstances, it's a _bad idea_ to change the type of a variable. The "proper" thing to do is to just create a new one.
- Languages that aren't dynamically typed are [statically typed](https://developer.mozilla.org/en-US/docs/Glossary/Static_typing), such as Go (which you'll learn in a later course). In a statically typed language, if you try to assign a value to a variable of the wrong type, an error would crash the program.

### Math With Strings 
- When working with strings the `+` operator performs a "[concatenation](https://en.wikipedia.org/wiki/Concatenation)", which is a fancy word that means "joining two strings". _Generally speaking, it's better to use string interpolation with `f-strings` over `+` concatenation_.

### Multi-Variable Declaration:
- We can save space when creating many new variables by declaring them on the same line:
```py
sword_name, sword_damage, sword_length = "Excalibur", 10, 200
```
- Any number of variables can be declared on the same line, and variables declared on the same line _should_ be related to one another in some way so that the code remains easy to understand.

### Functions:
- Functions allow us to _reuse_ and _organize_ code. 
- But we want to _reuse_ our code! Why would we want to redo our work? What if we wanted to calculate the area of thousands of circles??? **That's where functions help.**
- Instead, we can define a new function called `area_of_circle` using the `def` keyword.

```python
def area_of_circle(r):
    pi = 3.14
    result = pi * r * r
    return result
```
- Functions can have multiple parameters ("parameter" being a fancy word for "input").
- The name of a parameter doesn't matter when it comes to which values will be assigned to which parameter. It's **position** that matters. The first parameter will become the first value that's passed in, the second parameter is the second value that's passed in, and so on.
- Some new developers get hung up on the difference between `print()` and `return`.
- It can be particularly confusing when the test suite we provide simply prints the output of your functions to the console. It makes it _seem_ like `print()` and `return` are interchangeable, _but they are not_!
- `print()` is a function that:
    1. Prints a value to the console
    2. Does _not_ return a value
- `return` is a keyword that:
    1. Ends the current function's execution
    2. Provides a value (or values) back to the caller of the function
    3. Does _not_ print anything to the console (unless the return value is later `print()`ed)

- Code executes in _order from top to bottom_, so a variable needs to be created before it can be used. That means that if you define a function, you can't call that function until _after_ the definition.
- When no return value is specified in a function, it will automatically return `None`. For example, maybe it's a function that prints some text to the console, but doesn't explicitly return a value.
- A function can return more than one value by separating them with commas.
 ```python 
def cast_iceblast(wizard_level, start_mana):
    damage = wizard_level * 2
    new_mana = start_mana - 10
    return damage, new_mana # return two values
```
- When calling a function that returns multiple values, you can assign them to multiple variables.
```python
dmg, mana = cast_iceblast(5, 100)
print(f"Damage: {dmg}, Remaining Mana: {mana}")
# Damage: 10, Remaining Mana: 90
```
- To reiterate, **arguments are the actual values** that go into the function, such as `42.0`, `"the dark knight"`, or `True`. **Parameters are the names** we use in the function definition to refer to those values, which at the time of writing the function, can be whatever we like. 
- In Python you can specify a [default](https://docs.python.org/3/glossary.html#term-parameter) value for a function argument. It's nice for when a function has arguments that are "optional". You as the function definer can specify a specific default value in case the caller doesn't provide one.

- A default value is created by using the assignment (`=`) operator in the function signature.

```python
def get_greeting(email, name="there"):
    print("Hello", name, "welcome! You've registered your email:", email)
```

### Scope:
- Scope refers to _where_ a variable or function name is available to be used. For example, when we create variables in a function (such as by giving names to our parameters), that data is _not_ available outside of that function.

```python
def subtract(x, y):
    return x - y
result = subtract(5, 3)
print(x)
# ERROR! "name 'x' is not defined"
```
- So far we've been working in the global scope. That means that when we define a variable or a function, that name is accessible in _every other place_ in our program, even within other functions. 
### Testing and Debugging:
- A unit test is just an automated program that tests a small "unit" of code. Usually just a function or two. The editor will have tabs: the "main.py" file containing your code, and the "main_test.py" file containing the unit tests.
- These new unit-test-style lessons will test your code's _functionality_ rather than its output. Our tests will call functions in your code with different arguments, and expect certain return values. If your code returns the correct values, you pass. If it doesn't, you fail.
- There are two reasons for this change:
	1. It's more realistic. In the real world, you'll be writing unit tests and running them against your code to make sure it works as expected.
	2. You can run and debug your code with `print` statements, and leave those print statements in when you submit. Unlike the output-based lessons, you won't have to remove your `print` statements to pass.
### Debugging:
- When you're working as a professional developer, you'll typically write code on your computer and test it by yourself before it's deployed to users.
- That first part of the process is called _debugging_. You write some code, run it, and if it doesn't work, you fix the bugs. You repeat this process until you're confident that your code works as expected.
- A stack trace (or "traceback") is a scary-looking error message that the Python interpreter prints to the console when it encounters certain problems. Stack traces are most common (at least for you right now) when you're trying to run invalid Python code.
### Loops:
- Loops are a programmer's best friend. Loops allow us to do the same operation multiple times without having to write it explicitly each time.
- A _"for loop"_ in Python is written like this:
```python
for i in range(0, 10):
    print(i)
```
- The body of a for-loop _must_ be indented, otherwise you'll get a syntax error.
- Python has another type of loop, the `while` loop. It's a loop that continues `while` a condition remains `True`. The syntax is simple:
```python
while 1:
    print("1 evaluates to True")
```

### Lists:
- A natural way to organize and store data is in a `List`. Some languages call them "arrays", but in Python we just call them lists. Think of all the apps you use and how many of the items in the app are organized into lists.
- For example:
	- An X (formerly Twitter) feed is a list of posts
	- An online store is a list of products
	- The state of a chess game is a list of moves
	- This list is a list of things that are lists
- Lists in Python are declared using square brackets, with commas separating each item:

```python
inventory = ["Iron Breastplate", "Healing Potion", "Leather Scraps"]
```
- Sometimes when we're manually creating lists it can be hard to read if all the items are on the same line of code. We can declare the list using multiple lines if we want to.
- In the world of programming, counting is a bit strange! We don't start counting at `1`, we start at `0` instead.Each item in a list has an index that refers to its spot in the list.
- Now that we know how to create new lists, we need to know how to access specific items in the list.
- We access items in a list directly by using their _index_. Indexes start at 0 (the first item) and increment by one with each successive item. The syntax is as follows:
```python
best_languages = ["JavaScript", "Go", "Rust", "Python", "C"]
print(best_languages[1])
# prints "Go", because index 1 was provided
```
- The length of a List can be calculated using the `len()` function.The length of the list is equal to the number of items present. Don't be fooled by the fact that the length is not equal to the index of the last element, in fact, it will always be one greater.
- We can also change the item that exists at a given index. For example, we can change `Leather` to `Leather Armor` in the `inventory` list in the following way:
```python
inventory = ["Leather", "Iron Ore", "Healing Potion"]
inventory[0] = "Leather Armor"
```
- It's common to create an empty list then fill it with values using a loop. We can add values to the end of a list using the `.append()` method:

```python
cards = []
cards.append("nvidia")
cards.append("amd")
# the cards list is now ['nvidia', 'amd']
```
- `.pop()` is the opposite of `.append()`. Pop removes the last element from a list and returns it for use. For example:

```python
vegetables = ["broccoli", "cabbage", "kale", "tomato"]
last_vegetable = vegetables.pop()
# vegetables = ['broccoli', 'cabbage', 'kale']
# last_vegetable = 'tomato'
```
- While `.pop()` typically removes the last item of a list, it can also be used to remove an item at a specific index. For example, vegetables.pop(1) would remove 'cabbage' from the list. This can be useful when you need to remove items from other positions in your list.
- Remember that we can [iterate](https://en.wiktionary.org/wiki/iterate) over all the elements in a list using a loop. For example, the following code will print each item in the `sports` list.
```python
for i in range(0, len(sports)):
    print(sports[i])
```
- Python has _the most elegant_ syntax for iterating directly over the items in a list without worrying about index numbers. If you don't need the index number you can use the following syntax:
```python
trees = ['oak', 'pine', 'maple']
for tree in trees:
    print(tree)
# Prints:
# oak
# pine
# maple
```
- 