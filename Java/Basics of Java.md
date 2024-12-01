This page has all the basic concepts of java in brief. For the full explanation and deep understanding of the concepts go to its sources mentioned below them.

## Static keyword in Java

* In Java, when we declare a field _static_, exactly a single copy of that field is created and shared among all instances of that class.
* Doesn't matter how many times we instantiate a class, there will always be only one copy of static field belonging to it.
* From the memory perspective, static variables are stored in the heap memory
* You have to use the keyword static to make the variable, method or inner class as static.
* Basically, static method and variables belongs to class and not object of that class, so to call the methods you always have to use the class name and call them directly.
* Static methods and variables can't be overridden. **This is because _static_ methods in Java are resolved at compile time, while method overriding is part of Runtime Polymorphism**.
* Its really useful for creating utility and helper classes. Some popular JDKs Collections or Math utility classes.
* The following combinations of the instance, class methods, and variables are valid:
	1. instance methods can directly access both instance methods and instance variables
	2. instance methods can also access _static_ variables and _static_ methods directly
	3. _static_ methods can access all _static_ variables and other _static_ methods
	4. _static_ methods can’t access instance variables and instance methods directly. They need some object reference to do so.

## Heap memory in Java



