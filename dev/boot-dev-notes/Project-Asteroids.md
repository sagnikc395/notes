---
title: Asteroids Project
date: 6/1/25
tags:
  - boot-dev
  - basic-programming
  - pygame
  - python
---
### Modules:
- In Python, each `.py` file is a module, and we can import functions, variables, and classes from one module into another with the [`import`](https://docs.python.org/3/reference/simple_stmts.html#import) statement. The name of a module is the filename (without the `.py` extension).

```python
# import the function_hello function
# and the variable_player variable
# into the current file
from module import function_hello, variable_player
```
- If you want to import _everything_ from a module, you can use the `*` character:

```python
# import everything from a module
# into the current file
from module import *
```
###  Constants

- Games often have a lot of [magic numbers](https://en.wikipedia.org/wiki/Magic_number_(programming)) to represent things like player speeds, item costs, and attack damage. We will use this file as a place to store those kind of constant values.

### Game Loop:
- Video games are generally built using a [game loop](https://gameprogrammingpatterns.com/game-loop.html). The simplest game loop has 3 steps:

1. Check for player inputs
2. Update the game world
3. Draw the game to the screen

- To create a good user experience, these 3 steps need to happen _many times per second_.