---
title: Minimal Computer handling simple C programs
tags:
  - compilers
  - c-compiler
  - project-ashtar
date: 16/1/25
---
### The Four Compiler Passes:
- Lexer breaks up the source code into a list of tokens. Tokens are the smallest syntactic units of a program: they include delimiters, arithmatic symbols, keywords and identifiers. If a program is like a book, tokens are like individual words.
- Parser converts the list of tokens into a AST -> Abstract Syntax Tree, which represents the program in a form we can easily traverse and analyze.
- Assembly generation pass converts the AST into assembly. At this stage, we still represent the assembly instructions in a data structure that the compiler can understand ,not as text.
- Code emission pass writes the assembly code to a file so the assembler and linker can turn it to an executable.
### Hello, Assembly !
```c 
int main(void) {
return 2;
}
```
- This has a single function, main, containing a single return stmt, which will return a integer (here 2).
- To convert into assembly :
```shell 
$ gcc -S -O -fno-asynchronous-unwind-tables -fcf-protection=none return_2.c
```
- the compiler flags mean:
	- -S -> dont run the assembler or linker. This will make the compiler emit assembly instead of a binary file.
	- -O -> optimize the code. This will eliminate some instructions we aren't concerned with right now.
	- -fno-asynchronous-unwind-tables -> Don't geenrate the unwind table, which is used for debugging.
	- -fcf-protection=none -> disables control flow protection,a security feature that will add extra instructions we aren't concerned with. Control flow protection might already be disabled by default on our system.
- Finally the assembly will be :
```asm 
.global main 
main:
	movl $2 , %eax 
	ret 
```
- Assembly programs have several kinds of statements:
	- .global main -> assembler directive, a statement that provides directions for the assembler.
	- Assembler directives always start with a period. 
	- main is here a symbol , a name of a memory address.
	- Symbols appear in assembly instructions as well as assembler directives, eg: jmp main jumps to whatever address the main symbol refers to.
- 