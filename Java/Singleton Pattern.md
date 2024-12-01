## Basic idea

It is a creational design pattern that lets you ensure that a class has only one instance, while providing a global access point to this instance.

* Its a helpful technique when you need global variable or a single instance for whole program.
* The main problem with global variable is that any program can manipulate it. This makes it prone to errors. By adding singleton pattern we can avoid global variables being changed

## Steps to implement the pattern

All implementations of the Singleton have these two steps in common:

- Make the default constructor private, to prevent other objects from using the `new` operator with the Singleton class.
- Create a static creation method that acts as a constructor. Under the hood, this method calls the private constructor to create an object and saves it in a static field. All following calls to this method return the cached object.

If your code has access to the Singleton class, then it’s able to call the Singleton’s static method. So whenever that method is called, the same object is always returned.

## When to Use

* Use the Singleton pattern when a class in your program should have just a single instance available to all clients; for example, a single database object shared by different parts of the program.
* Use the Singleton pattern when you need stricter control over global variables.



Sources:
1. https://refactoring.guru/design-patterns/singleton

Learn more:
1. You can learn about static key works from this page: [[Basics of Java]] 