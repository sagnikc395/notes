- Advanced Typescript

## Pick:
 - pick allows us to create a new type by selecting a set of properties (Keys) from an existing type (Type).

## Partial:
 - Partial makes all properties of a type optional, creating a type with the same properties, but each marked as optional.
 - Especially useful when we want to do updates.

## Readonly:
 - **compile time checking, not runtime checking**
 - when we have a configuration object that should be altered after initialization, making it Readonly ensures that its properties cannot be changed.

## Record and Map
 - ### Record:
   - gives us a cleaner type to primitive objects.
 - ### Maps:
   - maps gives us a fancier way to deal with object. similar to Maps in cpp. 

## Exclude:
 - in a function that can accept several types of inputs , we want to exclude specific types from being passed to it.