## 1. Single responsibility principle:

Every class should have a single job to do. To be precise, there should be only one reason to change a class.
```java
public class Vehicle {    
public void printDetails() {}    
public double calculateValue() {}    
public void addVehicleToDB() {}
}
```

The `Vehicle` class has three separate responsibilities: reporting, calculation, and database. By applying SRP, we can separate the above class into three classes with separate responsibilities.

## 2. Open-closed Principle:

Software entities should be open for extension, but closed for modification.
```java
public class VehicleCalculations {    
public double calculateValue(Vehicle v) {        
if (v instanceof Car) {            
return v.getValue() * 0.8;        
if (v instanceof Bike) {            
return v.getValue() * 0.5;    
}}
```

Suppose we now want to add another subclass called `Truck`. We would have to modify the above class by adding another if statement, which goes against the Open-Closed Principle.
A better approach would be for the subclasses `Car` and `Truck` to override the `calculateValue` method:

```java
public class Vehicle {    
  public double calculateValue() 
  {...}
}

public class Car extends Vehicle {    
 public double calculateValue() {        
  return this.getValue() * 0.8;
}

public class Truck extends Vehicle{    
  public double calculateValue() {        
  return this.getValue() * 0.9;
}
```

## 3. Liskov substitution principle:

Derived types must be completely substitutable for their base types. Every base class should be easily replacable with its child/derived class. 

My understanding:

Child classes should be made in such a way that it agrees and accepts all the conditions provided by parent class.

For example: Square and rectangle. 

### why

This avoids misusing inheritance. Its helps us confirm to the "is-a" relationship
```java
public class Rectangle {    

private double height;    
private double width;    

public void setHeight(double h) 
{ height = h; }    

public void setWidht(double w) 
{ width = w; }    ...

}

public class Square extends Rectangle {    
public void setHeight(double h) {        
super.setHeight(h);        
super.setWidth(h);    
}    
public void setWidth(double w) {        
super.setHeight(w);        
super.setWidth(w);    
}}
```

The above classes do not obey LSP because you cannot replace the `Rectangle` base class with its derived class `Square`. The `Square` class has extra constraints, i.e., the height and width must be the same. Therefore, substituting `Rectangle` with `Square` class may result in unexpected behavior.

## 4. Interface segregation principle

The **Interface Segregation Principle (ISP)** states that clients should not be forced to depend upon interface members they do not use. In other words, do not force any client to implement an interface that is irrelevant to them.

Interfaces should be broken down into smaller pieces. By doing so, we can ensure that implementing classes only need to be concerned about the methods that are of interest to them.
  
Don’t pollute interfaces  
• Avoid fat interfaces  
• Interfaces here do not mean Java Interfaces.  
They mean the public methods that are exposed  
by a class.  

Suppose there’s an interface for vehicle and a `Bike` class:

```java
public interface Vehicle {    
public void drive();    
public void stop();    
public void refuel();    
public void openDoors();
}

public class Bike implements Vehicle {    
// Can be implemented    
public void drive() {...}    
public void stop() {...}    
public void refuel() {...}        

// Can not be implemented    
public void openDoors() {...}}
```

As you can see, it does not make sense for a `Bike` class to implement the `openDoors()` method as a bike does not have any doors! To fix this, ISP proposes that the interfaces be broken down into multiple, small cohesive interfaces so that no class is forced to implement any interface, and therefore methods, that it does not need.

## 5. Dependency Inversion Principle:

The **Dependency Inversion Principle (DIP)** states that we should depend on abstractions (interfaces and abstract classes) instead of concrete implementations (classes). The abstractions should not depend on details; instead, the details should depend on abstractions.

Consider the example below. We have a `Car` class that depends on the concrete `Engine` class; therefore, it is not obeying DIP.

```java
public class Car {    private Engine engine;    public Car(Engine e) {        engine = e;    }    public void start() {        engine.start();    }}public class Engine {   public void start() {...}}
```

The code will work, for now, but what if we wanted to add another engine type, let’s say a diesel engine? This will require refactoring the `Car` class.  
However, we can solve this by introducing a layer of abstraction. Instead of `Car` depending directly on `Engine`, let’s add an interface:

```java
public interface Engine {    public void start();}
```

Now we can connect any type of `Engine` that implements the Engine interface to the `Car` class:

```java
public class Car {    private Engine engine;    public Car(Engine e) {        engine = e;    }    public void start() {        engine.start();    }}public class PetrolEngine implements Engine {   public void start() {...}}public class DieselEngine implements Engine {   public void start() {...}}
```