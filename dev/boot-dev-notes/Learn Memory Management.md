---
title: Learning Memory Management
date: 12/1/25
tags:
  - boot-dev
  - c
  - memory-management
  - fundamentals
---
### Memory Management:
- Understanding how your _software_ runs on _hardware_ is important for writing fast, performant code. In this course we'll be talking all about one of the main aspects of software performance: **memory management**.
- Goals:
	1. **Understand how and where programs store data in memory**. Variables, functions and objects don't get to exist for free. Where do they live as your code runs?
	2. **Learn how to make programs more efficient**. Most performance related problems in backend software are memory related (at least in my experience). Learn how it all works so you can troubleshoot and optimize.
	3. **Practice programming in a lower-level language**. C gets you much closer to the hardware than Python, JavaScript, or Go. By writing C, you'll learn a lot about how software works closer to the metal.
	4. **Learn about garbage collection (and build your own)**. You will likely work in a garbage collected language at some point, whether that's Python, Go, JavaScript or something else. Best to understand what trade-offs are being made.

### C Basics:
- Hello world in C:
```c
#include <stdio.h>

int main() {
    printf("Starting the Sneklang interpreter...\n");
    return 0;
}

```
-  Python interpreter then executes that file top-to-bottom. If you have a `print()` at the top level, then it will print something.
- The entire file is _interpreted line by line_, _but that's not how C works_.
- The simplest C program is essentially:

```c
int main() {
    return 0;
}
```
- - A function named `main` is _always_ the entry point to a [C program](https://www.youtube.com/watch?v=tas0O586t80) (unlike Python, which enters at the top of the file).
- `int` is the return type of the function and is short for "integer". Because this is the `main` function, the return value is the [exit code](https://en.wikipedia.org/wiki/Exit_status) of the program. `0` means success, anything else means failure.
    - You'll find a lot of abbreviations in C because 1) programmers are lazy, and 2) it used to matter how many bytes your source code was.
- The opening bracket, `{` is the start of the function's body (C ignores whitespace, so indentation is just for style, not for syntax)
- `return 0` returns the `0` value (an integer) from the function. Again, this is the exit code because it's the `main` function.
    - `0` represents "nothing bad happened" as a return value.
- The pesky `;` at the end of `return 0;` is required in C to terminate statements.
- The closing bracket, `}` denotes the end of the function's body.