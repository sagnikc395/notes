---
title: Go for Developers
date: 8/2/25
tags:
  - boot-dev
  - golang
---
### Variables:

#### Basic Variables:
- `bool`: a boolean value, either `true` or `false`
- `string`: a sequence of characters
- `int`: a signed integer
- `float64`: a floating-point number
- `byte`: exactly what it sounds like: 8 bits of data

- Declaring a variable the sad way:
```go
var mySkillIssues int 
mySkillIssues. = 42 
```
- The first line, `var mySkillIssues int`, defaults the `mySkillIssues` variable to its zero value, `0`. On the next line, `42` overwrites the zero value.

#### Short Variable Declarations:
- GOATed variable declaration:
```go
mySkillIssues := 42 
```
- The walrus operator, `:=`, declares a new variable and assigns a value to it in one line. Go can infer that `mySkillIssues` is an `int` because of the `42` value. Yay [type inference](https://en.wikipedia.org/wiki/Type_inference)!
- When to use the Walrus Operator ?
	- The `:=`, (walrus operator) should be used instead of [var](https://go.dev/tour/basics/9) style declarations basically anywhere possible. The limitation is that `:=` can’t be used outside of a function (in the [global/package scope](https://dave.cheney.net/2017/06/11/go-without-package-scoped-variables) which we’ll talk about later).
- Type inference is based on the value being assigned.

#### Comments
- Go has two styles of comments:

```go
// This is a single line comment

/*
  This is a multi-line comment
  neither of these comments will execute
  as code
*/
```

#### Compilation Process
- Computers need machine code, they don’t understand English or even Go. We need to convert our high-level (Go) code into machine language, which is really just a set of instructions that some specific hardware can understand. In your case, your CPU.

- The Go compiler’s job is to take Go code and produce machine code, an `.exe` file on Windows or a standard executable on Mac/Linux.

- Go's program structure:
	- `package main` lets the Go compiler know that we want this code to compile and run as a standalone program, as opposed to being a library that’s imported by other programs.
	- `import "fmt"` imports the [`fmt` (formatting) package](https://pkg.go.dev/fmt) from the [standard library](https://pkg.go.dev/std). It allows us to use `fmt.Println` to print to the console.
	- `func main()` defines the `main` function, the entry point for a Go program.
- 2 kinds of bugs:
	- **Compilation Errors**: Occurs when code is compiled. It's generally better to have compilation error because they'll accidently make it into production. You can’t ship a program with a compiler error because the resulting executable won’t even be created.
	- **Runtime errors.** Occur when a program is running. These are generally worse because they can cause your program to crash or behave unexpectedly.

#### Same Line Declarations:
- We can declare multiple variables on the same line in golang.
```go 
mileage, compnay := 80276, "Toyota"
```

#### Small Memmory Footprint:
- 