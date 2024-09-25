---
title: Functional Programming Definitions
tags:
  - functional-programming
  - ocaml
date: 20/9/24
---
### Functors,Applicatives and Monads:
- ref: https://adueck.github.io/blog/functors-applicatives-and-monads-with-pictures-in-typescript/
- when we apply a function to a given value, we get different results depending on the context.
- The idea is based on the Maybe data type:
 ```ts 
 type Nothing = null;
 type Just<A> = {just: A};
 type Maybe<A> = Nothing | Just<A>;
```
#### Functors:
- When a value is wrapped in a context, we can't apply a normal function on it.
- here the concept of fmap comes from Haskell. fmap will know how to apply the functions to values that are wrapped in a context.
```ts 
const fmapMaybe = <A,B>(f: (a: A) => B, m: Maybe<A>): Maybe<B> => {
	if(!m){
		return undefined;
	} 
	return {just: f(m.just);}
}
```
- Functor is basically a typeclass:
	- Typeclasses is a sort of interface that defines some behaviour. If a type is a part of typeclass, that means that it supports and implements the behaviour the typeclass describes. They are like interfaces but better.
- A Functor is any data type that will define how an fmap applies to it. In TS, we dont have typeclasses, so we have to think of a functor as any data type that we have a fmap-like function defined for.
	- ![[Screenshot 2024-09-20 at 6.36.39 PM.png]]
- fmap will magically apply the function, because Maybe is a Functor. It will specify how fmap applies to Justs and Nothings ... however this is just for Haskell world.
- In TS, we can't just use fmap for any type of Functor.(unless making a big function and then using type narrowing for whatever type of Functor we throw at it.)
- If we want a data type to be a Functor, we need to define a fmap - like function for it.
- Behind the scenes:
	- First it will unwrap the the value from the context.
	- It will then apply the function.
	- get the result.
	- then again rewrap the value in context.
- for fmapMaybe for a Nothing type:
	- Unwrap nothing value.
	- Don't apply to a function.
	- This will end up with a nothing.
- Similarly we can apply the fmap to lists too, as lists are also functors. In TS, we use Array , and Array is a functor because it has a method called Array.map() which works as fmap for arrays.
- similarly we can extrapolate fmap on function and this  basically becomes function composition.
```ts
function compose<A, B, C>(f: (a: A) => B, g: (b: B) => C): (a: A) => C {
	return function (x: A): C {
	return g(f(x));
	};
}

function fmapFunction<A, B, C>(f: (a: A) => B, g: (b: B) => C): (a: A) => C{
  return compose(f, g);
}
```
#### Applicatives:
- With applicatives, our values are wrapped in a context, just like Functors.
- but our functions are also wrapped into a context too!
- In Haskell, <\*> , which knows how to apply a function wrapped in a context to a value wrapped in a context.
- This operator is often called the ``apply`` operator.
```ts
function applyMaybe<A, B>(f: Maybe<(a: A) => B>, m: Maybe<A>): Maybe<B> {
  // if the function Maybe is Nothing, return Nothing
  if (f === undefined) {
    return undefined;
  }
  // if the data Maybe is Nothing, return Nothing
  if (m === undefined) {
    return undefined;
  }
  // else apply the function in the Maybe
  // to the data in the Maybe
  return { just: f.just(m.just) };
}
```

- <\*> function then takes each of the functions in the list and applies them to all of the values in the other list.
```ts
function applyArray<A,B>(fa: ((a: A) => B)[],arr:A[]): B[] {
	//applying each function in the array 
	// to each element in the other array 
	return fa.flatMap(f => arr.map(f));
}
```
- Applicative can take any function that expects any number of unwrapped values. Then when we pass it all the wrapped values and we get back a wrapped value.
- 