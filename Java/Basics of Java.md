This page has all the basic concepts of java in brief. For the full explanation and deep understanding of the concepts go to its sources mentioned below them.

## Data types

#### Primitive Data types

Java has 8 primitive data types:

| Type      | Size (bits) | Minimum | Maximum        | Example                         | notes                                            |
| --------- | ----------- | ------- | -------------- | ------------------------------- | ------------------------------------------------ |
| _byte_    | 8           | -27     | 27– 1          | _byte b = 100;_                 | a compact data type, great for conserving memory |
| _short_   | 16          | -215    | 215– 1         | _short s = 30_000;_             | larger than byte                                 |
| _int_     | 32          | -231    | 231– 1         | _int i = 100_000_000;_          | used for whole numbers                           |
| _long_    | 64          | -263    | 263– 1         | _long l = 100_000_000_000_000;_ | for representing long numbers                    |
| _float_   | 32          | -2-149  | (2-2-23)·2127  | _float f = 1.456f;_             | floating-point numbers with single precision     |
| _double_  | 64          | -2-1074 | (2-2-52)·21023 | _double f = 1.456789012345678;_ | floating-point numbers with double precision     |
| _char_    | 16          | 0       | 216– 1         | _char c = ‘c’;_                 |                                                  |
| _boolean_ | 1           | –       | –              | _boolean b = true;_             |                                                  |
source: https://www.baeldung.com/java-primitives#:~:text=2.-,Primitive%20Data%20Types,about%20memory%20management%20in%20Java).

## Type casting


## var keyword in Java

It allows you to create a variable without explicitly declaring the specific data type of the variable. This keyword forces automatic type inference based on the type of the assigned value, so it necessary to provide the value of variable at the time of declaration.

### When to use?

With `var` , we don’t have to reiterate what is obvious, hence, we simply use `var` for the local variable. Also the `var` keyword uses type inference because of which it can identify the type of the variable depending on the value assigned to it.

When you use the traditional approach, your code will be difficult to read because in most of the cases there will be type duplications, for example,

`EmployeeDetail employeeDetail = new EmployeeDetail ();`

With using `var` , the code will become much more readable and concise. Let’s compare this with the example above.

`var employeeDetail = new EmployeeDetail ();`

### When not to use?

* You cannot declare a local variable using `var` without initializing it or with `null` value.
* You cannot use `var` for declaring instance fields, static fields, declaring a lambda expression, parameters for constructors or methods, method return types and generic types.
* When you want same type of variable for an object of same inheritance hierarchy,

### Conclusion

In a nutshell, the var keyword look like a really good way to improve readability and reduce the length of the code by not stating which is obvious. We can use this with local variables, or with objects where automatic inference makes sense.


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



