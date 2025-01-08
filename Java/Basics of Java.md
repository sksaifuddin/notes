**This** page has all the basic concepts of java in brief. For the full explanation and deep understanding of the concepts go to its sources mentioned below them.

## Data types

### Primitive Data types

Java has 8 primitive data types:

1) byte - 8 bits
2) short - 16 bits
3) int - 32 bits
4) long - 64 bits
5) float - 32 bits
6) double - 64 bits
7) char - 16 bits
8) boolean - 1 bit
### Type casting

Type Casting is changing the data type. Suppose you need to assign a value of one type to a variable of another type. Meaning, you need to cast the source type to target type

source type -> target type

#### Implicit casting

The compiler automatically performs casting when target type is wider than the source type.

source type -> target type (wider) // can do automatic casting

This direction of implicit casting is:
byte -> short -> int -> long -> float -> double

example:

```java
int num = 100;
long bigNum = num; // 100L
```

#### Explicit Casting

Incase source is wider than the target type then the casting cannot be done by the compiler, the programmer has to explicitly mention the casting types.

To perform explicit casting, a programmer must write the target type in parentheses before the source.
```java
(targetType) source
```

In this case there will be loss in the data, this is called "Type Overflow", because the source was actually holding more data than the target data, so its very important to be really careful when doing explicit casting.

### Primitive and reference types

In java, all data types are separated into two groups: primitive types and reference types. 

Java can have two data types. The eight primitive types and reference types. Reference types can be made by users and also there are some in build reference types.

#### new keyword

The reference types can be created using the keyword "new". What is essentially does is it allocates memory for the objects we create. This step of allocating memory for objects is called "instantiation" (creating memory for object and then assigning to a variable) because we create an instance of the object. 

```java
String language = new String("java"); 
//instantiation of String and initialization with "java"
```

You can also use a literal for strings:

```java
String language = "java";
```

#### Main difference

The main difference between reference types and primitive types is in the memory. Primitive types stores the actual values, where as the reference types stores an address of the memory where the data is located.

To difference is in Heap and stack memories. The primitive types are stored in stack memory, but variables of reference types store addresses of objects located in heap memory.

![Heap and stack](https://drive.google.com/file/d/1pVomefdpWiJ16Ua2JAAki5zr9K_w8YT1)

There is one more difference is that reference types can have null assigned to them which tells us that it is not initialized yet. The means a variable is created but still there is no memory created for the object in the heap, only after the new keyword it will be created.

### Floating-point types

Floating point types basically represents decimal/ fractional numbers. A floating point numeral generally refers to the notation of a number which contains an integer part, a fractional part and their separator (example: 1.03; 1 = integer part, . = separator, and 03 = fractional part)

In Java, you can represent this number in two ways "float" and "double". They can store limited number of decimal numbers (6-7 for float and 14-16 for double). Always try to use double when you need to represent fractions, its more safe.

We need to use the character f with floating numbers.

```java
float pi = 3.1415f;
float negValue = -0.15f;
System.out.println(pi); // 3.1415 without f
```

You have to be careful when using floating numbers because it can cause errors.
for example:
```java
double d = 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1;
System.out.println(d); // it prints 0.9999999999999999 // actual : 1
```

Such errors happen because floating point numbers are actually stored and operated in binary form and not all real numbers can be represented exactly

### Constants. Final variables

Sometimes, you need to use a variable that should not be modified during the program. Such variables are called constants. Java provides a special keyword called final to declare them.

The only difference between the normal variable and the final variable is that you cannot modify or reassign the value once assigned.

```java
final double PI = 3.1415;
```

#### Final reference variables

The final keyword can be legally used with reference variables. This means that it not possible to reassign a reference to the variable. But you can still change the internal state of the object. This is similar to the constant in javascript, so it should be easier to understand.

Here is an example with the `StringBuilder` class which is a mutable version of `String`.

```java
final StringBuilder builder = new StringBuilder();
builder = new StringBuilder(); // error line

builder.append("Hello!"); // it works 
System.out.println(builder.toString()); // Hello!
```

But unlink JS, we don't usually make all variables constant in java instead we do it only when required.

### Increment and Decrement

In Java we have two operators to increase and decrease the value. The most difficult part for me to understand was always difference between postfix and Prefix

#### Prefix and Postfix forms

Both increment and decrement operators have two forms, which are very important when using the result in the current statement:

- the **prefix** form (`++n` or `--n`) increases or decreases the value of a variable before it is used;
- the **postfix** form (`n++` or `n--`) increases or decreases the value of a variable after it is used.

The following examples demonstrate both forms of increment.

**Prefix increment:**
```java
int a = 4;
int b = ++a;

System.out.println(a); // 5
System.out.println(b); // 5
```

In this case, the value of `a` has been incremented and then assigned to `b`. So, `b` is 5.

**Postfix increment:**
```java
int a = 4;
int b = a++;

System.out.println(a); // 5
System.out.println(b); // 4
```

In Java, the postfix operator has higher [precedence](https://hyperskill.org/learn/step/5008 "In Java, precedence refers to the order of performing and grouping operations in an expression. | Operations with higher precedence are performed before those with lower precedence. For example, multiplication and division have a higher precedence than addition and subtraction. Parentheses can be used to specify the order of execution and can be nested. Additionally, there is a precedence order of all arithmetic operators, including parentheses, with unary plus/minus having the highest level of precedence, followed by multiplication and division, and then addition and subtraction.") than the [assignment operator](https://hyperskill.org/learn/step/5008 "In Java, an assignment operator is a symbol used to assign a value to a variable. | The most common assignment operator is the single equals sign (=), which assigns the value on the right to the variable on the left. For example, in the statement `int x = 10;`, the assignment operator is used to assign the value 10 to the variable x. It's important to note that the assignment operator should not be confused with the equality operator (==), which is used to test for equality between two expressions.").

### Difference in comparison operators == and equals

You should never compare the primitive types using comparison operators. When you are comparing two variables of type String (reference type), it compares references (addresses) rather than the actual values. Correct way is to compare the content using equals method on the string.

### var keyword in Java

It allows you to create a variable without explicitly declaring the specific data type of the variable. This keyword forces automatic type inference based on the type of the assigned value, so it necessary to provide the value of variable at the time of declaration.

#### When to use?

With `var` , we don’t have to reiterate what is obvious, hence, we simply use `var` for the local variable. Also the `var` keyword uses type inference because of which it can identify the type of the variable depending on the value assigned to it.

When you use the traditional approach, your code will be difficult to read because in most of the cases there will be type duplications, for example,

`EmployeeDetail employeeDetail = new EmployeeDetail ();`

With using `var` , the code will become much more readable and concise. Let’s compare this with the example above.

`var employeeDetail = new EmployeeDetail ();`

#### When not to use?

* You cannot declare a local variable using `var` without initializing it or with `null` value.
* You cannot use `var` for declaring instance fields, static fields, declaring a lambda expression, parameters for constructors or methods, method return types and generic types.
* When you want same type of variable for an object of same inheritance hierarchy,

#### Conclusion

In a nutshell, the var keyword look like a really good way to improve readability and reduce the length of the code by not stating which is obvious. We can use this with local variables, or with objects where automatic inference makes sense.

## Methods
### Overloading in Java

Having multiple methods with same but different parameters is called Method overloading. It has same name but have distinct arguments. When a method is called , the language determines which version of the method to run based on the number, types and order of the arguments.

It is an essential concepts in OOPs that makes code more concise, easier to read and maintain and enable its reuse.

### Array as parameters

This is really important to understand. When you pass the primitive types to a method, you are passing a value but when you pass array which is a reference type, a copy of the reference is created, but the values is the same. This means that if you change the actual value (elements of an array) in the body of a method, you will see these changes outside the method.

The following method swaps the first and the last elements of its parameter (array).

```java
public static void swapFirstAndLastElements(int[] nums) { // nums is an array
    if (nums.length < 1) {
        return; // it returns nothing, i.e. just exits the method
    }

    int temp = nums[nums.length - 1]; // save the last element in a temporary local variable
    nums[nums.length - 1] = nums[0];  // now, the last element becomes the first
    nums[0] = temp;                   // now, the first element becomes the former last
}
```

Calling the method from the main method:

```java
public static void main(String[] args) {

    int[] numbers = { 1, 2, 3, 4, 5 }; // numbers

    System.out.println(Arrays.toString(numbers)); // before swapping

    swapFirstAndLastElements(numbers); // swapping

    System.out.println(Arrays.toString(numbers)); // after swapping
}
```

The output is:

```java
[1, 2, 3, 4, 5]
[5, 2, 3, 4, 1] 
```

So, in the body of the main method, an array is visible as modified.

### Varargs

It is passible to pass any number of same type of arguments to a method using a special syntax named varargs (variable-length arguments), This is the syntax: "..." (three dots). In the body of the method, you can process this parameter as a regular array of specified type.

The following method takes an integer **vararg** parameter and outputs the number of arguments in the standard output using the **length** property of arrays.

```java
public static void printNumberOfArguments(int... numbers) {
    System.out.println(numbers.length);
}
```

As you can see, a special syntax `**...**` is used here to specify a **vararg** parameter.

Now, you can invoke the method by passing several integer numbers or an array of ints.

```java
printNumberOfArguments(1);
printNumberOfArguments(1, 2);
printNumberOfArguments(1, 2, 3);
printNumberOfArguments(new int[] { }); // no arguments here
printNumberOfArguments(new int[] { 1, 2 });
```

This code outputs:

```java
1
2
3
0
2
```

This example also demonstrates the difference between the arguments and parameters of a method. The method has only a single parameter but it can be called with several arguments.

Varargs should always last one in the declaration of the method.
Here is an incorrect example:

```java
public static void method(double... varargs, int a) { /* do something */ }
```

The correct version of the method is:

```java
public static void method(int a, double... varargs) { /* do something */ }
```


## Object Oriented Programming


Object Oriented programming centers around classes and objects and cornerstones.

### Classes and Objects

Classes serves as a blueprint, much like architectural plans that are used when constructing multiple buildings.

A class encapsulates data so that the object and methods can manipulate the data. An object is a specific instance of a class. We can create an object of the class using new keyword.

### Grouping classes with packages




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



