---
title: Common Programming Concepts
tags:
  - rust
  - rust-basic-types
  - rust-control-flow
  - rust-functions
date: 15/6/25
---
### Keywords:
- Rust language has a set of keywords that are reserved for use by the language only, much as in other languages. We cannot use these words as names of variables or functions. Most of the keywords have special meanings, and we will be using them to do various tasks in our Rust programs.

## Variables and Mutability
### Intro about variables and mutability:
- Variables are immutable by default in Rust. This is one of the many nudges that Rust gives us to write our code in a way that takes advantage of the safety and easy concurrency that Rust offers. 
- However, we still have the option to make our variables mutable using the `mut` keyword.
```rust 
fn main() {
	let mut x = 5;
	println!("The value of x is :{x}");
	x = 6; 
	println!("The value of x is : {x}");
}
```
- We are allowed to change the value bound of x from 5 to 6 when mut keyword is used. 

### Constants:
- Constants are values that are bound to a name and are not allowed to change, but there are a few differences between constants and variables.
- Differences between constants and non-mut:
	- Constants are not just immutable by default -> they are always immuable. We declare constants using the `const` keyword instead of the `let` keyword and the type of the value must be annotated. 
	- Constants can be declared in any scope, including the global scope, which makes them useful for values that many parts of code need to know about.
	- Constants may be only set to a constant expression, not the result of a value that could only be computed at runtime.Eg:
	```rust
	 const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;
	```
- Rust naming convention for constants is to use all uppercase with underscores in between the words. The compiler is able to evaluate a limited set of operations at compile time, which lets us choose to write out this value in a way that's easier to understand and verify, rather than setting this constant to the value.
- Constant's are valid for the entire time a program runs, within the scope in which they were declared. This property makes constants useful for values in our application domain that multiple parts of the program might need to know about, such as the maximum number of points any player of a game is allowed to run, or the speed of light.
- Naming hardcoded values used throughout our program as constants is useful in conveying the meaning of that value to future maintainers of the code. It also helps to have only one place in our code we would need to change if the hardcoded value needed to be updated in the future.

### Shadowing:
- In `mut` example, the first variable is shadowed by the second, which means that the second variable is what the compiler will see when we use the name of the variable. In effect, the second variable overshadows the first, taking any uses of the variable name to itself until either it itself is shadowed or the scope ends.
```rust 
fn main() {
	let x = 5;
	let x = x + 1;
{
	let x = x * 2;
	println!("The value of x in the inner scope is : {x}");
}
	println!("The value of x is :{x}");
}
```
- Shadowing is different from marking a variable as `mut` since we'll get a compile time error if we accidently try to reassign to this variable without using the let keyword. By using let , we can perform a few transformations on a value but have the variable be immutable after those transformations have been completed.
- Another diff bw mut and shadowing is that since we are effectively creating a new variable when we use the `let` keyword again, we can change the type of the value but reuse the same name -> only that we are not allowed to change the variable's underlying type.
```rust 
let spaces = "  ";
let spaces = spaces.len();
```

### Data Types:
- Every value in Rust is of a certain data type, which tells Rust what kind of data is being specified so it knows how to work with that data. 
- Rust is a statically typed programming langs, which means it must know the types of all variables at compile time. The compiler can usually infer what types we want to use based on the value and how we use it. In cases, when many types are possible, such as when we converted a `String` to a numeric type using `parse` , we must add a type annotation:
```rust
let guess: u32 = "42".parse().expect("Not a number!");
```