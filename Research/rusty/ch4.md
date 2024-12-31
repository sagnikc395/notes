---
title: Understanding Ownership
tags:
  - rust
  - rust-ownership
  - compilers
d: 28/12/24
---
### What is Ownership ?
- Ownership is a set of rules that govern how a Rust program will manage the memory. Since all programs have to manage the way they use a computer's memory, some pl have garbage collection in their runtimes , in other languages , the programmer must explicitly allocate and free the memory.
- Rust manages the memory through a system of ownership with a set of rules that the compiler checks. If any of the rules are violated, the program then wouldnt compile.
- Before understanding ownership, we must first understand the differences bw stack and heap and how is memory managed.
### Stack and Heap:
- Both stack and the heap are parts of memory available to our code to use at runtime, but they are structured in different ways. 
- Stack stores the values in the order it gets them and removes the values in the opposite order.(LIFO fashion)
	- All the data stored on the stakc must have a known ,fixed size.
- Data with unknown size at compile time or a size that might change(think vectors, maps etc.) must be stored on the heap instead.
	- heap is less organized : when you put data on the heap,you request a certain amount of space. The memory allocator finds an empty spot in the heap that is big enough,marks it as being in use, and returns a pointer, which is the address of that location.
	- This is called as allocating on the heap.
	- Since the pointer to the heap is known fixed size, we can store the pointer itself on stack, but when we want the actual data, we must follow the pointer.
- Pushing on the stack is faster than allocating on heap because the allocator never has to search for a place to store new data : the location is always at the top of the stack.
- Similarly allocating space on the heap requires more work because the allocator must first find a big enough space to hold the data and then perform bookkeeping to prepare for the next allocation.

- Ownership addresses the problems of keeping track of what parts of code are using what data on the heap,minimizing the amount of duplicate data on the heap, and cleaning up unused data on the heap so that we don't run out of space are all problem that ownership addresses.

### Ownership Rules:
- The rules are:
	- Each value in Rust has a owner.
	- There can only be one owner at a time.
	- When the owner goes out of scope, the value will be dropped.

### Variable Scope:
- Scope is the range within a program for which an item is valid. Eg:
```rust 
let s = "hello";
```
- Variable s refers to a string literal, where the value of the string is hardcoded into the text of our program. The variable is valid from the point at which it's declared until the end of the current scope. 
- Imp things to note:
	- When s comes into scope, it is valid.
	- It remains valid until it goes out of scope.
### String Type:
- String type is a datatype whose size is known not known at runtime , and needs to be stored on the heap.
- String literals is where a string value is hardcoded into our program. String literals are convinient ,but they aren;t suitable for every situation for every situation in which we may want to use text.
- What if we want to take user input and store it ? String type. This type manages data allocated on the heap and as such is able to store an amount of text that is unknown to us at compile time. This type manages data allocated on the heap and as such is able to store an amount of text that is unknown to us at compile time.
```rust
let s = String::from("hello");
```
- :: using this as a namespace this particular from function under the String type rather than using some sort of name like string_from.
- This kind of string can be mutated also:
```rust 
let mut s = String::from("hello");
s.push_str(", world!");
println!("{s}");
```

### Memory and Allocation:
- With the String type , in order to support a mutable,growable piece of text, we need to allocate an amount of memory on the heap, unknown at compile time,to hold the contents.Meaning that :
	- The memory must be requested from the memory allocator at runtime. (done from String::from)
	- We need a way of returning this memory to the allocator when we are done with our String. -> In most langs , GC keeps track of and cleans up memory that isn't being used anymore. 
	- Rust takes a different path: the memory is automatically returned once the variable that owns it goes out of scope.
- Natural point at which we can return the memory our String needs to the allocator: when s goes out of scope. When a variable goes out of scope, Rust calls a special function for us. This function is called `drop` , and it's where the author of String can put the code to return the memory. Rust will call drop automatically at the closing curly braces.

#### Variables and Data Interacting with Move:
- Multiple variables can interact with the same data in different ways in Rust.
```rust 
let x = 5;
let y = x;
```
- since the size is known at compile time, we can store this in stack and this will point to different areas in memory.
- while 
```rust 
let s1 = String::from("hello");
let s2 = s1;
```
- this stores in heap as the size is not known in compile time.
- i.e the second line would make a copy of the value in s1 and bind to s2. But this is not what quite happens.
- String is made up of three parts:
	- A pointer to the memory that holds the contents of the string 
	- a length : how much memory in bytes (the contents of the String are currently using)
	- a capacity : total amount of memory in bytes that the String has received from the allocator.
- This group of data is stored on the stack.
- When we assign s1 to s2 , the String data is copied , meaning we are copying the pointer, the length and the capacity that are on the stack. We do not copy the data on the heap that the pointer refers to.
- However as we noted previously that when a variable goes out of scope, Rust will automatically call the drop function and clear up the heap memory for that variable. In our current scenario, when s2 and s1 both go out of scope, they will both try to free the same memory. This is known as a **double free error**.
- To prevent this when we do `let s2 = s1`, Rust will consider s1 as no longer valid. Therefore ,Rust doesnt need to free anything when s1 goes out of scope.
- Shallow Copy := Concept of copying the pointer, length and capacity without copying the data.

#### Scope and Assignment:
- The inverse rule of this relationship between ownership, scoping and memory being freed via the drop function is also true. When we assign a completely new value to an existing variable, Rust will call the drop and free the original value's memory immediately.
```rust 
let mut s = String::from("hello");
s = String::from("ahoy");

println!("{s}, world!");
```
#### Variables and Data Interacting with Clone:
- If we want to deeply copy the heap data of the String, not just the Stack data, we can use a common method called clone. 
```rust 
let s1 = String::from("hello");
let s2 = s1.clone();
```