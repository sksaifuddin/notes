Design smells are certain structures in the design that indicate violation of  fundamental design principles and negatively impact design quality.

### Principle of Abstraction:

Hiding all but relevant data about an object in order to reduce complexity and increase efficiency.

==!Dont just think abstraction as just abstract classes, it can just be classes or any kind of implemenation hiding technique==

## Why do you have a complete abstraction?

An important abstract implementation is to create a cohesive and complete abstraction. When the abstraction does not support related methods, it may affect the cohesion and integrity of the abstraction. If the abstraction only supports some related methods, its users may have to implement other functions themselves. The client program may attempt to directly access the abstract internal implementation details, and the side effect is to violate the encapsulation principle.

SOURCE: https://medium.com/@mena.meseha/incomplete-multifaceted-unused-and-repeated-abstraction-7902b093e4ab

### 1. Missing abstraction: (There is no abstraction at all)

 - This smell arises when dumps of data or encoded strings are used instead of creating a class or an interface.
	- You just create string or other data kind which is not so useful. Good way is to create a class or an interface for every structure.
	- example: Throwable class in JDK
	- ```public class Throwable {  
		public void printStackTrace();  
		//other methods elided.  
		}  ```
	- Initially java had only printStackTrace which will just print the stack trace. It was difficult for people to identify the error from pile of code. It was later modified as following:
	- ```public class Throwable {  
		public void printStackTrace();  
		public StackTraceElement[] getStackTrace();  
		//other methods elided.  
		}  
		public final class StackTraceElement {  
		public String getFileName();  
		public int getLineNumber();  
		public String getClassName();  
		public String getMethodName();  
		public boolean isNativeMethod();  
	}```
	- This abstraction now was really helpful for debugging.

### 2. Incomplete abstraction:

This bad smell is caused when the abstract does not support all complementary or related methods. (Two complimentary functions/implemenations should be binded together). If they are related or compliminetary and not together then it can effect cohesiveness and will be called "Incomplete abstraction".
![](https://drive.google.com/file/d/1xOWBfoyZxzhFU8zhuUbYiS62QsSRp2je/view?usp=sharing)
![incomplete abstarction | 300](https://drive.google.com/uc?export=view&id=1xOWBfoyZxzhFU8zhuUbYiS62QsSRp2je)

For example, from the classes above, setUserObject and getUserObject are complimentary methods but are in two different abstractions, which will make it difficult to use them. This is called incomplete abstraction.

SOURCE: 
1. https://medium.com/@mena.meseha/incomplete-multifaceted-unused-and-repeated-abstraction-7902b093e4ab
2. Professor's PPTs


### 3. Deficient Abstraction:

Declared accessibility of one or more members of abstraction is more persmissive that actually required. (Too many public method / access modifiers, which allows client to use it although it should have been not allowed. User can then misuse it, so its better to hide that implementation which is not required by the user).

### 4. Multifaceted Abstraction:

This smells arises when an abstraction has more than one responsibility assigned to it. This violates single responsiblity principle and should be avoided.

#### How to solve?
When a class assumes multiple responsbilities, it is not cohesive. You can use the "extract class" for refactoring.



[[Abstraction design smells]]

