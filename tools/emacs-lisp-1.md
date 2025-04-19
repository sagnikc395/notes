---
title: Practicel Emacs Lisp Tutorial 1
date: 18/4/25
tags:
  - emacs-lisp
  - lisp
  - emacs
---
#### What is Emacs Lisp ?
- Programming language that forms the foundation of Emacs text editor. Allows users to interact ,customize and extend emacs functionality.

#### Running Emacs Lisp
- Open a empty buffer and type the command and put the cursor over the end of the line and type C-x C-e.
- Lisp's order of operations is akin to Reverse-Polish-Notation(RPN).
```emacs 
( - 2 (+ 3 4))
```
- here perform the minus operation on 2 and (+ 3 4), where (+ 3 4) means perform the + operation on 3 and 4.
- Similarly we can call functions in the same way, ex: we could press M-x describe-bindings.

#### Flow Control 
- structure of an basic if/else in Emacs lisp is 
```lisp
(if (condition) 
	(execute if condition true)
	(execute if condition false))
```
- Print something out based on if your current line number
```lisp
(if (eq (what-line) "Line 20")
(princ "Im at line 20")
(princ "Im not at line 20"))
```

#### Writing Functions 
- The defun keyword is used to define a function.
```lisp 
(defun function-name (parameter1 parameter2 etc.)
(code to execute))
```
- Function to taking 2 numbers and adding them together:
```lisp 
(defun add-numbers (num1 num2)
(+ num2 num1))
```

- and then we can invoke it with:
```emacs 
(add-numbers 3 5)
```

#### Interacting with Emacs:
- 