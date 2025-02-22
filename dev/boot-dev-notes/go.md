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

#### Go is Statically Typed:
- Go enforces [static typing](https://developer.mozilla.org/en-US/docs/Glossary/Static_typing) meaning variable types are known _before_ the code runs. That means your editor and the compiler can display type errors before the code is ever run, making development easier and faster.
- Contrast this with most dynamically typed languages like JavaScript and Python... Dynamic typing often leads to subtle bugs that are hard to detect. The code _must_ be run to catch syntax and type errors. (sometimes in production if you're unlucky 😨)
- Two strings can be [concatenated](https://en.wikipedia.org/wiki/Concatenation) with the `+` operator. But the compiler will not allow you to concatenate a `string` variable with an `int` or a `float64`.

#### Compiled vs Interpreted:
- You can run a compiled program _without_ the original source code. You don't need the compiler anymore after it's done its job. That's how most video games are distributed! Players don't need to install the correct version of `Go` to run a PC game: they just download the executable game and run it.
- With interpreted languages like Python and Ruby, the code is interpreted at [runtime](https://en.wikipedia.org/wiki/Runtime_\(program_lifecycle_phase\)) by a separate program known as the "interpreter". Distributing code for users to run can be a pain because they need to have an interpreter installed, and they need access to the source code.
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
- Go programs are fairly lightweight. Each program includes a small amount of extra code that's included in the executable binary called the [Go Runtime](https://go.dev/doc/faq#runtime). One of the purposes of the Go runtime is to clean up unused memory at runtime. It includes a [garbage collector](https://en.wikipedia.org/wiki/Garbage_collection_\(computer_science\)) that automatically frees up memory that's no longer in use.
- As a general rule, Java programs use _more_ memory than comparable Go programs. There are several reasons for this, but one of them is that Java uses a virtual machine to interpret bytecode at runtime and typically allocates more on the [heap](https://courses.grainger.illinois.edu/cs225/fa2022/resources/stack-heap/).
- On the other hand, Rust and C programs use slightly _less_ memory than Go programs because more control is given to the developer to optimize the memory usage of the program. The Go runtime just handles it for us automatically.

#### Constants:
- Constants are declared with the `const` keyword. They can't use the `:=` short declaration syntax.
```go 
const pi = 3.14159
```
- Constants can be primitive types like strings, integers, booleans and floats. They _can not_ be more complex types like slices, maps and structs, which are types we will explain later.
- Constants must be known at compile time. They are _usually_ declared with a static value.
- However, constants _can be computed_ as long as the computation can happen at _compile time_.
- Eg:
```go 
const firstName = "Lane"
const lastName = "Wagner"
const fullName = firstName + " " + lastName
```
- you _cannot_ declare a constant that can only be computed at run-time like you can in JavaScript.

#### Comparing Go's Speed:
- Go is _generally_ faster and more lightweight than interpreted or VM-powered languages like:
	- Python
	- JavaScript
	- PHP
	- Ruby
	- Java
- In terms of execution speed, Go does lag behind some other compiled languages like:
	- C
	- C++
	- Rust
- Go is a bit slower mostly due to its automated memory management, also known as the "Go runtime". Slightly slower speed is the price we pay for memory safety and simple syntax!

#### Formatting Strings in Go:
- Go follows the [printf tradition](https://cplusplus.com/reference/cstdio/printf/) from the C language. In my opinion, string formatting/interpolation in Go is _less_ elegant than Python's f-strings, unfortunately.
	- [fmt.Printf](https://pkg.go.dev/fmt#Printf) - Prints a formatted string to [standard out](https://stackoverflow.com/questions/3385201/confused-about-stdin-stdout-and-stderr).
	- [fmt.Sprintf()](https://pkg.go.dev/fmt#Sprintf) - Returns the formatted string
- %v variant prints the Go syntax representation of a value , it's a nice default :
```go 
s := fmt.Sprintf("I am %v years old", 10)
// I am 10 years old

s := fmt.Sprintf("I am %v years old", "way too many")
// I am way too many years old
```
- string:
```go 
s := fmt.Sprintf("I am %s years old ","way too many")
```
- Integer:
```go 
s := fmt.Sprintf("I am %d years old", 10)
// I am 10 years old
```

- Float: 
```go 
s := fmt.Sprintf("I am %f years old", 10.523)
// I am 10.523000 years old

// The ".2" rounds the number to 2 decimal places
s := fmt.Sprintf("I am %.2f years old", 10.523)
// I am 10.52 years old
```

#### Runes and String Encoding:
- In many programming languages (cough, C, cough), a "character" is a single byte. Using [ASCII](https://www.asciitable.com/) encoding, the standard for the C programming language, we can represent 128 characters with 7 bits. This is enough for the English alphabet, numbers, and some special characters.
- In Go, strings are just sequences of bytes: they can hold arbitrary data. However, Go also has a special type, [`rune`](https://go.dev/blog/strings), which is an alias for `int32`. This means that a `rune` is a 32-bit integer, which is large enough to hold any [Unicode](https://home.unicode.org/) code point.
- When you're working with strings, you need to be aware of the encoding (bytes -> representation). Go uses [UTF-8](https://en.wikipedia.org/wiki/UTF-8) encoding, which is a variable-length encoding.

#### What does this mean ?
- 2 main takeaways here :
	1. When you need to work with individual characters in a string, you should use the `rune` type. It breaks strings up into their individual characters, which can be more than one byte long.
	2. We can include a wide variety of Unicode characters in our strings, such as emojis and Chinese characters, and Go will handle them just fine. 


### Conditionals:
#### Conditionals:
- `if` statements in Go do not use parentheses around the condition:
```go 
if height > 4 {
fmt.Println("You are tall enough !")
}
```

- else if and else are supported as we might expect:
```go 
if height > 6 {
	fmt.Println("You are super tall!")
} else if height > 4 {
	fmt.Println("You are tall enough")
} else {
	fmt.Println("You are not tall enough !")
}
```

#### Initial Statement of an If Block:
- An `if` conditional can have an "initial" statement. The variable(s) created in the initial statement are _only_ defined within the scope of the `if` body.
- Why to use this ?
	- bit shorter 
	- limits the scope of the initialized variable(s) to the if block.

```go 
if length := getLength(email);length < 1 {
	fmt.Println("Email is invalid")
}
```

#### Switch :
- Switch statements are a way to compare a value against multiple options. They are similar to if-else statements but are more concise and readable when the number of options is more than 2.
- Notice that in Go, the `break` statement is not required at the end of a `case` to stop it from falling through to the next `case`. The `break` statement is implicit in Go.
```go 
func getCreator(os string) string {
	var creator string 
	switch os {
		case "linux":
		creator = "Linus Torvalds"
		case "windows":
		creator = "Bill Gates"
		case "mac":
		creator = "A Steve"
		default:
		creator = "Unknown"
	}
	return creator
}
```