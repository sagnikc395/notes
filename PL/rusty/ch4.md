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
- When we see a call to clone, we know that some arbitary code is being executed and that code may be expensive.

#### Stack-Only Data: Copy
- Types like integers that have a known size at compile time are stored entirely on the stack, so copies of the actual values are quick to make.
```rust 
let x = 5;
let y = x;
```

- No reason we would want to prevent x from being valid after we have created the variable y. In other words,there is no difference bw deep and shallow copying here, so calling clone would not do anything different from the usual shallow copying, and we can leave it out.

- Copy Trait:
	- we can place it on types that are stored on the stack.
	- If a type implements the Copy trait, variables that use i do not move, but rather are trivially copied, making them still valid after assignment to another variable.
	- However if a type or any of its parts has implemented the Drop trait, we cannot implement the Copy trait.
	- If the type needs something special to happen, when he values goes out of scope and we add the COpy annotation to that type, we will get a compile-time error.

- Some types that implement the Copy trait:
	- All integer types (u32)
	- Boolean type (bool) with values true and false
	- All floating point types (f64) 
	- Character Type (char) 
	- Tuples if they only contain types that also implement Copy.
### Ownership and Functions:
- Passing a variable to a function will move or copy, just as assignment does. 

```rust 
fn main() {
	let s = String::from("hello");
	takes_ownership(s);

	let x = 5; 
	makes_copy(x);
}
//x going out of scope, then s, but since s's values was moves, nothing special happens 

fn takes_ownership(some_string: String) {
	println!("{some_string}");
}

fn makes_copy(some_integer: i32) {
	//integer comes into the scop
	println!("{some_integer}");
}
// some_integer goes out of scope. nothing special happens

```
- If we use s after the call to takes_ownership, Rust would throw a compile-time error. These static chekcs protects us from mistakes.
### Return Values and Scopes:
- Return values can also transfer ownership. 
- Ownership follows the same pattern every time (for a  variable):
	- assigning a value to another variable moves it.
	- When a variable that includes data on the heap goes out of scope, the value will be cleaned up by drop unless ownership of the data has been moves to another variable.
- What if we wnat to let a functon use a value but not take ownership?
	- Quite annoying that anything we pass in also needs to be passed back if we want to use it again, in addn to any data resulting from the body of the function that we might want to return as well.
	- We can use a tuple to return multiple values.

- Instead of writing this boilerplate , we can use a value without transferring ownership, using references.
### References and Borrowing:

- Reference is like a pointer in that it's an address we can follow to access the data stored at that address; that data is owned by some other variable.
- Unlike a pointer, a reference is guranteed to point to a valid value of a particular type for the life of that reference.
- When we pass &s1 into the function name and defn as &String, we pass a references and they allow us to refer to some value without taking ownership of it.
- Opposite of referecing is deferencing and repr by * operator.

```rust 
let s1 = String::from("hello");
let len = calculate_length(&s1);
```
- &s1 syntax lets us create a refernce that refers to the value of s1 but doesn't own it. Since it doesnt own it, the value it points to will not be dropped when the reference stops being used.

- **Inside the function**:
	```rust 
	fn calculate_length(s: &String) -> usize {
		s.len()
	}
	//here s will go out of scope,but since it does not have ownership of what it refers to, it is not dropped.
	```
	- scope in which the variable s is valid is the same as any function's parameter scope, but the value pointed to by the ref is not dropped when s stops being used, since s doesn't have ownership.
	- When functions have references as parameters instead of the actual values, we won't need to return the values in order to give back ownership, since we never had ownership.

- **Borrowing**: Action of creating a reference. As in real life, if a person owns something, we can borrow it from them. When we are done, we have to give it back, since we dont own it.

- Like variables are immutable by default, so are references. We are not allowed to modify something we have a reference to.

#### Mutable References:
- Like variables ,we can add mut keyword i.e &mut s, where we call the change function, and update the function signature to accept a mutable reference with some_string: &mut String.
- change function will mutate the value it borrows.

- **Restriction**:
	- if we have a mutable reference to a value, we cannot have no other references to that value.
	```rust 
	
	let mut s = String::from("hello");

	let r1 = &mut s;
	let r2 = &mut s;
	println!("{}, {}",r1,r2);
	```
	- The first mutable borrow is in r1 and must last until we used in the println!, but bw the creation of that mutable reference and its usage, we tried to create another mutable reference in r2 that borrows the same data as r1.

- **preventing data races**:
	- Restriction preventing multiple mutable references to the same data at the same time allows for mutation but in a very controlled manner.
	- Benefit of having this restriction is that Rust can prevent data races at compile time. A data race is similar to a race condition and happens when these three beaviours occur:
		- 2 or more pointers access the same data at the same time.
		- At least one of the pointers is being used to write to the data.
		- There is no mechanism being used to sync access to the data.

- We can use curly brackets to create new scope, allowing for multiple mutable references,just not simultaneous ones.

- Also we cannot have a mutable reference while we have an immutable ones to the same value.
- Users of an immutable reference don't expect the value to suddenly change out from under them! Multiple immutable references are allowed since no-one who is just reading the data has the ability to affect anyone else's reading of the data.

#### Dangling References:
- Languages like C, where we are able to directly access the pointer ,very easy to erroneusly create a dangling pointer - a pointer that references a location in memory that may have been given to someone else - by freeing some memory while preserving a pointer to that memory.
- In Rust, the compiler gurantees the references will never be dangling references: if we have a reference to some data, the compiler will ensure that the data will not go out of scope before the reference to the data does.

#### Rules of Reference:
- At any given time, we can either have 1 mutable refernece of any number of immutable references.
- References must always be valid.
### Slices:
- Slice lets us reference a contiguous sequence of elements in a collection rather than the whole collection. 
- A slice is kind of reference, so it does not have ownership.
- iter is a method that returns each element in a collection and that enumerate wraps the result of item and returns each element as part of a tuple instead.
- First element of the tuple returned from enumerate is the index and the second element is a reference to the element. This is a bit more convenient than calculating the index ourselves.
- Since enumerate method returns a tuple, we can use patterns to destructure that tuple. 
#### String Slices:
- More elegant way to solve the same thing.
- String slice is a reference to part of a String, looks like:
```rust 
let s = String::from("hello world");

let hello = &s[0..5];
let world = &s[6..11];
```
- Rather than reference to the entire string, hello here is a refrence to a portion of String.
- We create slices using a rane within brackets by specifying starting_index and ending_index, where starting_index is the first position in the sluce and endin_index is one more than the last position in the slice.
- Internally, the slice data structure stores the starting posn and the length of the slce, corresponding to ending_index minus starting_index. 
- With Rust's .. range syntax,if we want to start at index 0, we can drop the value before the 2 periods.
```rust 
let s = String::from("hello");
let len = s.len();

//slice and slice_2 are the same
let slice = &s[0..2];
let slice_2 = &s[..2];
let slice_3 = &s[3..len];
let slice_4 = &s[..];
```
- 