---
title: Enums and Pattern Matching
tags:
    - rust 
    - pattern-matching
    - enums
    - compilers
date: 23/1/25
--- 

### Defining and Enum:
- While structs gives us a way of grouping together related fields and data , enums gives us a way of saying a value is one of a possible set of values.
- Eg: Since there are only 2 possibiliteis of an IP address that our program will come across, we can enumerate all possible variants , which is enumeration gets its name.
- Any enum can either v4 or v6, but not both at the same time. That property of IP addresses makes the enum data structure appropriate because an enum value can only be one of its variants.
```rust 
enum IpAddrKind {
    V4,
    V6
}
```
- IpAddrKind is now a custom data type, that we can use elsewhere in our code.

#### Enum Values:
- We can create instances of each of the 2 variants of IpAddrKind:
```rust
let four = IpAddrKind::V4;
let six = IpAddrKind::V6;
```
-  Using enums has other advantages also:
    - At the moment , we don't have a way to store the actual IP address data, we only know what kind it is.
    - also repr the data using just an enum is more concise: rather than an enum inside a struct, we can put data directly into each enum variant. This new repr of data , says that v4 and v6 variants will have associated String values
    ```rust
    
    enum IpAddr {
        V4(String),
        V6(String),
    }

    let home = IpAddr::V4(String::from("127.0.0.1"));
    let loopback = IpAddr::V6(String::from("::1"));
    ```
    - here easier to see anothe rdetail oh how enums work: name of each enum variant that we define also becomes a function that constructs an instance of the enum. i.e IpAddr::V4() is a function call that takes a String argument and returns an instance of the IpAddr type. 
    - Each variant can have different types and amounts of associated data.
    ```rust 

    enum IpAddr {
        V4(u8,u8,u8,u8),
        V6(String),
    }

    let home = IpAddr::V4(127,0,0,1);
    let loopback = IpAddr::V6(String::from("::1"));
    ```
- Similarity bw enums and structs:
    - just as we are able to define methods on structs using impl, we are also able to define methods on enums.
    ```rust 
    impl Message {
        fn call(&self){
            //method boyd would be defined here 
        }
    }

    let m = Message::Write(String::from("hello"));
    m.call();
    ```
    - Body of the method would use self to get the value that we called the method on.
### Option Enum:
- Another enum defined by the standard library. The Option type encodes the very common scenario in which a value could be something or it could be nothing.
- Eg: requesting the first item in a non-empty list, we would get a value. If we request the first item in an empty list, we would get nothing. Expressing this concept in terms of the type system means the compiler can check whether we have handled all the cases we should be handling -> this functionality can prevent bugs that are extremely common in other programming langs.
- Problem with null values is that if we try to use a null value as a not-null value, we will get an error of some kind. Because this null or not-null property is pervaise, extremely easy to make this kind of error.

- Rust doesn't have nulls, but it does have an enum that can encode the concept of a value being present of absent:
```rust 
enum Option<T> {
    None,
    Some(T),
}
```
- `Option<T>` is so pervasive that it's included in the prelude, we don't need to bring it into scope explicitly. The variants of Option are also included in the prelude: we can use Some and None directly without the Option:: prefix. `Option<T>` enum is still just a regular enum, and `Some(T)` and `None` are still varians of it.
- `<T>` is a generic type parameter- meaning that the Some variant of the Option enum can hold one piece of data of any type, and that each concrete type that gets used in place of `T` makes the overall `Option<T>` type a different type.
```rust 
let some_number = Some(5);
let some_char = Some('e');

let absent_number: Option<i32> = None;
```
- Rust can infer these types because we have specified a value inside the `Some` variant. For `absent_number` , Rust requires us to annotate the overall `Option` type: the compiler can't infer the type that the corresponding `Some` variant will hold by looking only at a `None` value.
- When we have a `Some` value, we know that a value is present and the value is held within the `Some`. When we have a `None` value, in some sense it means the same thing as null: we don't have a valid value.
    - `Option<T>` and `T` are different types, the compiler won't let us use an `Option<T>` value as if it were definitely a valid value.

- In order to have a value that can possibly be null, we must explictly opt in by making the type of that value `Option<T>`. Then, when we use that value, we are required to explicitly handle the case when the value is null. Everywhere that a value has a type that isn't an `Option<T>` , we can safely assume that the value isn't null. 

- To use an `Option<T>` value, we want to have code that will handle each variant. We want some code that will run only when we have a `Some(T)` value, and this code is allowed to use the inner T.

- We want some other code to run only if we have a `None` value, and that code doesn't have a `T` value available.The `match` expression is a control flow construct that does just this when used with enums: it will run different code depending on which variant of the enum it has, and that code can use the data inside the matching value.
### match Control Flow Construct:
- match control flow that allows us to compare a value against a series of patterns and then execute code based on which pattern matches.
- Patterns can be made up of literal values, variable names, wildcards and many other things. Power of match comes from the expressiveness of the patterns and the face that compiler confirms that all possible cases are handled.

- Values go through each pattern in a match, and at the first pattern the value "fits", the value falls into the associated code lock to be used during execution.

- Unlike if expression, the condition needs to evaluate to a Boolean value,but here it can be any type. The type of coin in this example is the Coin enum.
- match arms:
    - Arm has 2 parts : a pattern and some code.First arm here has a pattern that is value `Coin::Penny` and then he `=>` operator that seperates the pattern and the code to run.
    - Each arm is seperated from the next with a comma.
    - When the `match` expression executes, it compares the resultant value against the pattern of each arm, in order. If a pattern matches the value, the code associated with that pattern is executed. If the pattern doesn't match the value, execution continues to the next arm.

- Code associated with each arm is an expression, and the resultant value of the expression in the matching arm is the value that gets returned for the entire match expression.

### Patterns that bind to values:
- Another useful feature of match arms is that they can bind to the parts of the values that match the pattern.

- in the value_in_cents, if we were to call value_in_cents`(Coin::Quarter(UsState::Alaska))`,coin would be `Coin::Quarter(UsState::Alaska)`. When we compare that value with each of the match arms, none of them match until we reach `Coin::Quarter(state)`.
- At that point, the binding for state will be the value `UsState::Alaska`. We can then use that binding in the println! expression, thus getting the inner state value  out of the Coin enum variant for `Quarter`.

### Mathching with `Option<T>`
- To get the inner T value out of the Some case when using `Option<T>` , we can also handle `Option<T>` using match , as we did with the Coin enum!
- Instead of comparing coins, we'll compare the variants of `Option<T>`, but the way the match expression works remain the same.

- Does Some(5) match Some(i) ?
    - it does ! We have the same variant. The i binds to the value contained in Some, so i takes the value 5.
    - The code in the match arm is then executed, so we add 1 to the value of i and create a new Some value with our total 6 inside.

- Second call of plus_one using None:
    - We enter the match and compare to the first arm:
    ```rust 
    None => None,
    ```

- It actually matches ! There is no value to add to, so the program stops and returns the None value on the right side of `=>`. Because the first arm matched, no other arms are compared.

- Combining `match` and enums is useful in many situations. We will see this pattern a lot in Rust code:
    - match against an enum, bind a variable to the data inside and then execute code based on it.
    - It's a bit tricky, but once we get used to it, we will wish we had it in all languages.

### Matches are Exhaustive
- There is none other aspect of match we need to discuss: the arm's patterns must cover all possibilities.
- Matches in Rust are exhaustive: we must exhaust every last possibility in order for the code to be valid.
- Especially in the case of `Option<T>` , when Rus prevens us from forgetting to explicitly handle the `None` case, it protects us from assuming that we have a value when we might have null, thus making the billion-dollar mistake discussed earlier impossible.

### Catching-all Patterns and _ placeholder:
```rust 
    let dice_roll = 9;
    match dice_roll {
        3 => add_fancy_hat(),
        7 => remove_fancy_hat(),
        other => move_player(other),
    }

    fn add_fancy_hat() {}
    fn remove_fancy_hat() {}
    fn move_player(num_spaces: u8) {}
```
- Using enums, we can also take special actions for a few particular vlaues, but for all other values takes one default action.
- The catch-all pattern meets the requirement that match must be exhaustive. Note that we have to put the catch-all arm last because the patterns are evaluated in order.If we put the catch-all arm earlier, the other arms would never run, so Rust will warn us if we add arms after a catch-all!
- Rust also has a pattern we can use when we want a catch-all but don't want to use the value in the catch-all pattern: 
    - _ is a special pattern that matches any value and does not bind to that value.
    - This tells Rust we aren't going to use the value, so Rust won't warn us about an unused variable.

### Concise Control Flow with if let 

- 