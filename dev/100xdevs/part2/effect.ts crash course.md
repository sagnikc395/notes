---
title: Effect Library Overview
tags:
  - web-dev
  - effect
date: 8/12/24
---
### Effect Core Concepts
- intro to core effect concepts
- real world examples by rewriting two apps
- peek into 'advanced' Effect.
### What is an 'Effect' ?
- an Effect is a description of a program that is lazy and immutable.
- **program** -> series of transformations that we can run to transform an given input to an output.
- **immutable** -> scripts are inherently immutable, if not changing the source, bun can directly write it and make changes to it.
- **laziness** -> programs are lazy meaning they are not evaluated until they are required to do so.
- Effect -> has all of these properties but made into a inside Javascript type. -> **Functions** (Effect is a description of a program that is lazy and immutable).
- Effect builds on top of what functions can offer !
- General definition of function:
```ts
type Function<Args, T> = (...args: Args) => T;
```
- however this does not encode the error type in the type definition which we encode => we would need to use try and catch, we wouldnt know what error is being thrown.
- instead,Effect works with errors as values kinda proposition.
- better defn using errors:
```ts
type SaferFunction<Args, T, E> = (...args: Args) => T | E;
```
- however this also comes with some problems as it becomes harder to discriminate errors.
```ts
declare function Foo(): "baz" | "bar" | Error;
const result = Foo();
const error = result instanceof Error;

declare function Foo2(): "baz" | "bar" ; 
const result2 = Foo2();
const error = result2 !== "baz";
```
- composing functions with errors:
	- inner function that might error and outer function that also might error
	- only operate on value if it is not an error.
	- here we have to manually check each error type.
```ts 
declare function Inner(): "baz" | "bar" | Error ;
function Outer(): number | Error {
const result = Inner();
if (result instanceof Error) {
return result;
}
return result.length;
}
```
- we are forced here to handle errors at every single point, even if we don't care.
### Effects are different :
- Effect type has 2 type parameter:
	- Value and Error(default to never)
```ts 
//example of how the effect type looks like 
type Effect<Value,Error = never> = /* .... */ ;
```
- i.e it has a default error type as never, meaning it cannot error.
- so we can transform our previous functions using the Effect type as  :
```ts
declare const foo: Effect<number, never>;
declare const bar: Effect<number, Error>;
```
- having errors as a first class citizens and owning errors , and can compose errors also.
- with Effects we kinda get the result, we can provide the dependency explicitly.
- benefits we get this from this are: we can mock it easily, provide a abstraction over the db class etc.
```ts 
// taking db as a parameter is useful and abstracts over the db instance 
function getUser(db: Database, id: number): User {
return db.users.getById(id);
}
```
- TBD: 15:26 