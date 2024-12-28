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
- 