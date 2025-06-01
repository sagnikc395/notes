---
tags:
  - program-synthesis
  - mit6S891
  - compilations
  - ai
date: 1/6/25
---
My notes for the MIT Course on [Introduction to Program Synthesis in Fall 2023](https://people.csail.mit.edu/asolar/SynthesisCourse/index.htm)

### Background:
- recently while I was listening to the Machine Learning Street Talk podcast, Francois Chollet was one of the guests talked about why he become a [proponent of program synthesis](https://www.youtube.com/watch?v=TQDCsyuuwsg)
> 	The premise of his observation on why program synthesis is the next frontier is that no matter how you try, neural networks and by extensions deep learning models will try to latch onto statistical regularities like statistical noise eventually and would not be able to implement the parsing of the program that we want to implement.
- Deep Learning is a good problem solving mechanism for some kinds of problems , like:
	- Pattern matching in continuous space, but was not going to do everything like create discrete symbolic programs.
	- To create better discrete symbolic programs there are better and more energy efficient ways to do so.
- If we face a problem which have continuous structure, then gradient descent is the right way to solve it, but in other cases not so much.


