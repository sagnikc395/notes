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

### Defining Modules to Control Scope and Privacy
- use keyword that will bring a path into scope.
- pub keyword to make items public.
- as keyword , external packages and glob operator.

#### Modules Cheat Sheet
- *Start from crate root*: When we compile a crate, the compiler will first look in the crate root file (src/lib.rs for library or src/main.rs for binary) for code to compile.
- *Declaring Modules* : in crate root file , we can declare new modules, eg: garden module with mod garden;. The compiler will look for the module's code in these places:
	- Inline -> within curly brackets that replaces the semicolon following mod garden.
	- In the file src/garden.rs 
	- In the file src/garden/mod.rs 
- *Declaring Submodules*: In any other file than the crate root, we can declare submodules. Eg: might declare mod vegetables; in src/garden.rs. The compiler will look for the submodule's code within the directory names for the parent module in these places:
	- inline -> directly following mod vegetables; within curly brackets instead of the semicolon .
	- in the file src/garden/vegetable.rs 
	- in the file src/garden/vegetable/mod.rs 
- *Paths to code in modules* : Once a module is part of our crate, we can refer to code in that module from anywhere else in that same crate, as long as the privacy rules allow, using the path to the code. Eg: Asparagus type in the garden vegetables modules would be found at crate::garden::vegetable::Asparagus.
- *Private vs Public*: Code within a. module is private from its parent modules by default. To make a module public, declare it wiht pub mod instead of mod. To make items within a public module public as well, use pub before their declarations.
- *use* : within a scope, use keyword creates shortcuts to items to reduce repetition of long paths. Eg: if we were previously requiring to do crate::garden::vegetables::Asparagus , now we would only be required to write Asparagus if we had imported using use

#### Grouping Related Code in Modules:
- Modules let us organize code within a crate for readability and easy reuse. 
- Modules also allows us to control the privacy of items because code within a module is private by default. Private items are internal implementation details not available for outside use. we can choose to make modules and the items within them public, which exposes them to allow external code to use and depend on them.
- Eg: using a resturant library project:
	- front of the house and back of the house
	- Front house is where customers are -> hosts seat customers , servers take orders and payment and bartenders make drinks.
	- Back hourse is where the chefs and cooks work in the kitchen, dishwashers clean up, and managers do admin work.

- To structure our crate this way, we can organize its functions into nested modules. 
	- we define a module using mod keyword and then the name of the module.
	- Body of the module then goes inside the curly brackets.
	- Inside modules we can place other modules, here hosting and serving.
	- Modules can also hold definitions for other items, like structs, enums ,constants,traits etc.

- By using modules, we can group related definitions together and name why they are related. Programmers using this code can navigate the code based on groups rather than having to read through all defns, making it easier to fin definitions relevant to them. 
- Programmers adding new functionality to the code would know where to place the code to keep the program organized.

- src/main.rs and src/lib.rs are called as crate roots because the contents of either of these 2 files form a module named crate at the root of the crate's module structure called the module tree.
- In resturant crate, hosting and serving are siblings defined within front_of_house. If module A is contained within module B, we say that module A is the child of module B and that module B is the parent of module A. Entire module tree is rooted under the implicit module named crate.

### Paths for referring to an Item in the Module Tree
- For Rust compiler to find an item in a module tree -> we need to find a path in the same way we use a path when navigating a filesystem.
- Path can take 2 forms:
	- *absolute path* -> full oath starting from a crate root ; for code from an external crate , absolute path begins with the crate name and for code from the current crate -> starts with literal crate.
	- *relative path* -> starts from the current module and uses self, super or an identifier in the current module.
- Both absolute and relative paths are followed by 1 or more identifiers seperated by double colons (::). 
- add_to_waitlist() in eat_at_resturant , we use an absolute path. add_to_waitlist function is defined in the same crate as eat_at_resturant , which means we can use the crate keyword to start an absolute path. We then include each of the successive modules until we make our way to add_to_waitlist. We can imagine a filesystem with the same structure : we'd specify the path `/front_of_house/hosting/add_to_waitlist` to run the add_to_waitlist program; using the crate name to strat from the crate root is like using `/` to start from the filesystem root in our shell.
- Choosing whether to use a relative or absolute path is a decision that we'll make based on our project and it depends on whether we are more likely to move item definition code separately from or together with the code that uses the item.Our prefrence in general is to specify absolute paths because it's more likely well want to move code definitions and item calls independently of each other.
- By default , in Rust, all items(functions,methods,structs,enums,modules and constants) are private to parent modules by default. If we want to make an item like a function or struct private, we put it in a module.
- Items in a parent module can't use the private items inside child modules, but items in child modules can use the items in their ancestor modules. 
- This is due to child modules wrap and hide their implementation details, but the child modules can see the contenxt in whcih they are defined. To continue wiht our metaphor, think of the privacy rules as like back office of a resturant -> what goes on is private to resturant customers, but office manages can see and do everything in the resturant they operate.
- Rust choose to have the module system function this way so that hiding inner implementation details is the default. This way, we would know which parts of the inner code we can change without breaking outer code.
#### Exposing Paths with the pub keyword:
- Adding pub keyword in front of mod hosting will make the module public. With this change, if we can access front_of_house , we can also access hosting. But the contents of hosting are still private, making the module public doesnt make its contents public.
- pub keyword on a module only lets the code in its ancestor module refer to it, not access its inner code. Because modules are containers, there is not much we can do by only making the module public -> we need to go further and choose to make one or more of the items within the module public as well.

- For relative path, rather than starting from crate root, the path starts from front_of_house. The front_of_house module is defined within the same module as eat_at_resturant, so the relative path starting from the module in which eat_at_resturant is defined works.
- 