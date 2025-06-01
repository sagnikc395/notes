---
title: Basis of Program Synthesis
tags:
  - program-synthesis
  - computation
  - compilations
  - ai
date: 1/6/25
---
### Historical Context :
- Traditionally, the way automation was incorporated into software development was through the use of compilers and high-level languages. 
- The first-program synthesizers emerged in logic-programming in 1969, where constraint solving techniques were modified to yield programs for certain types of specification.
- Hiatus of research in program synthesis ended in early 2000s when a number of independent pieces of work showed that synthesis could be made practical by taking advantages in automatic constraint solving techniques and by carefully restricting the synthesis problems to enable new clever search techniques.
- Eg: Automatic Spreadsheet manipulation in Microsoft Excel.
### Program Synthesis:
- An informal defn of program synthesis:
> 	Program Synthesis correspond to a class of techniques that are able to generate a program from a collection of artifacts that establish semantic and syntactic requirements for the generated code.
- Or more generally we can say it like:
> 	Program Synthesis is the task of automatically finding a program within a given search space (i.e a set of programs provided) that meets a given specification (i.e a user intent specified typically by a logical formula or a set of input-output examples).
> 	

### Synthesis vs ML , Synthesis vs Compilation, Synthesis vs Declarative Programming:
#### Synthesis vs Compilation:
- While compilation and synthesis are very closely related in terms of their goals, they both aim to support the generation of software from a HLD (high level description) of its behaviour , however a synthesizer is expected to do more than translate a program from one notation to another -> also know how to perform the desired task.
- **Search**:
	- In a compiler, an input description of the computation is transformed into a program by applying transformation rules according to pre-defined schedule.
	- In a synthesizer it is generally understood to involve a search for the program that satisfied the stated requirements.
	- Fuzzy lines as several modern research compilers aggresively search the space of transformations to find optimal implementations in a process known as Autotuning.
#### Synthesis vs Declarative Programming:
- TODO