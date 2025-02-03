---
title: Packages , Crates and Modules
tags:
  - rust
  - compilers
  - software-packaging
date: 2/1/25
---
- As we write large program, organizing code will become increasingly important. By grouping related functionality and seperating code with distinct features, we will clarify where to find code that implements a particular feature and where to go to change how a feature works.
- Rust has a number of features that allow us to manage our code's organization, including which details are exposed, which details are private and what names are in each scope in our programs. These features, sometimes collectively called to as the module system,include:
	- Packages : A Cargo feature that lets us build,test and share crates.
	- Crates: A tree of modules that produces a library or executable.
	- Modules and use : Lets us control the organization,scope and privacy of paths.
	- Paths: A way of naming an item, such as struct, function or module.

### Packages and Crates:
- A crate is the smallest amount of code that the Rust compiler considers at a time. Even if we run rustc rather than cargo and pass a single source code file, the compiler will consider that file to be a crate.
- Crates can contain modules, and the modules may be defined in other files that get compiled with the crate.
- There are 2 forms of a crate:
	- A binary crate 
		- programs that we can compile to an executable that we can run, such as command line program or a server. 
		- Each must have a function called main that defines what happens when the executable runs.
	- A library crate
		- don't have a main function , and they don't compile to an executable. 
		- Instead they define functionality intended to be shared with multiple projects.
		- Eg: rand crate provides functionality that generates random numbers. 
- Crate root is a source file that the Rust compiler starts from and makes up the root module of our crate.
- A package is a bundle of one or more crates that provides a set of functionality. A package contains a Cargo.toml file that describes how to build those crates.
- Cargo is actually a package that contains the binary crate for the CLI tool that we have been using to build our code. Cargo package also contains a library crate that the binary crate depends on.
- Other projects can depend on the Cargo library crate to use the same logic the Cargo CLI tool uses. A package can contain as many binary crates as we would like, but at  most only 1 library crate.
- A package must contain atleast 1 crate, whether its a library or binary crate.
- When we create a new binary project, Cargo creates a src directory that contains main.rs file. Cargo follows the convention that src/main.rs crate root of binary create with the same name as the package.
- Similarly , cargo knows that if the package directory contains src/lib.rs , the package contains a library crate with the same name as the package,and src/lib.rs is its crate root. 
- Cargo will pass the crate root files to rustc to build the library or binary.
- If a package contains src/main.rs and src/lib.rs , it will have 2 crates : a binary and a library,both with the same name as the pacakge. A package can have multiple binary crates by placing files in the src/bin directory: each file will be seperate binary crate.