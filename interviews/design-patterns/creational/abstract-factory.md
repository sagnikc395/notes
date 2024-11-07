---
title: Abstract Factory Pattern
tags:
  - design-patterns
  - typescript
---
### Abstract Factory Pattern 

- It is a creational design pattern that lets us produce families of related objects without specifying their concrete classes.

### Problem :
- Say, we are creating a furniture shop simulator. Our code consists of classes that represent:
	- A family of related produces -> Chair + Sofa + CoffeeTable 
	- Several variants of this family. -> Modern, Vicorian, ArtDeco
- We need a way to create individual furniture objects so that they can match other objects of the same family, and also we dont want to change our existing code when adding new products or families of products to the program. 

### Solution:
- Abstract Factory pattern suggests is to explicitly declare interfaces for each distinct product of the product family.
- We can then make all variants of products to follow those interfaces.
	- i.e all chair variants can implement the Chair interface, 
	- all coffee table variants can implement the CoffeeTable interface and so on.
- Next Move is to declare Abstract Factory -> an interface with a list of creation methods for all products that are part of the product family.
	- These methods must return abstract product types represented by the interfaces we extracted previously -> Chair, Sofa, CoffeeTable and so on.
- Now for each variants of a product family, we create a seperate factory class based on the AbstractFactory interface. A factory is a class that returns products of a particular kind. Eg: ModernFurnitureFactory can only create ModernChair, ModernSofa and ModernCoffeeTable objects.
- Client code has to work with both factories and products via their respective abstract interfaces. This lets us change the type of a factory that we pass to the client code, as well as the product variant that the client code receives , without breaking the actual client code.