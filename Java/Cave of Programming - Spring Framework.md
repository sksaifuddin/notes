
## Spring Framework and Spring Data JPA

### Spring Boot Hello World

You can create a maven or a gradle application and then import spring boot as dependency. This will give you quick idea about spring boot and how to do its basic setup

This is the official spring boot dependency link: https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter/3.4.0

Once you import the dependency into your maven/Gradle dependency file then create a new file in the src/main/java/app package called App.java

This App.java will be the entry point of the application. Add this code in the App.java
```
package app;  
  
import org.springframework.boot.SpringApplication;  
import org.springframework.boot.autoconfigure.SpringBootApplication;  
  
@SpringBootApplication  
public class App {  
    public static void main(String[] args) {  
        SpringApplication.run(App.class, args);  
    }  
}
```

This will create a spring boot application with an entry point. The spring boot application always starts from this point. It looks into SpringApplication.run and the class which has SpringBootApplication annotation.

### Entry Point

App.java is our entry point. Now we will create a spring boot component and add it to the application context.

Create a new class called Runner which implements CommandLineRunner interface and just implement its method to remove the compilation error. This will create a component which allows you to print to command line. But this is not enough we also have to tell spring boot to check for this component. So in the App.java add the scanBasePackages to the SpringBootApplication annotation and mention the package name.

This is how the updated code looks like:

Runner.java
```
package app;  
  
import org.springframework.boot.CommandLineRunner;  
import org.springframework.stereotype.Component;  
  
@Component  
public class Runner implements CommandLineRunner {  
  
    @Override  
    public void run(String... args) throws Exception {  
        System.out.println("Hello World!");  
    }  
}
```

App.java
```
package app;  
  
import org.springframework.boot.SpringApplication;  
import org.springframework.boot.autoconfigure.SpringBootApplication;  
  
@SpringBootApplication(scanBasePackageClasses = App.class)  
public class App {  
    public static void main(String[] args) {  
        SpringApplication.run(App.class, args);  
    }  
}
```

### Creating Beans

Typically in spring application we need one instance of various classes. We can use singleton objects, but spring provides a better alternative for it called Beans.

These classes which we have only one instance of is called Beans in spring lingo. Bean just means a instance of class which is present throughout out application and group of beans is container which is called Application context. So we will create a bean and add it to the application context to be able to use it in our application.

Create a class called Greeter with following code:
```
package app;  
  
public class Greeter {  
  
    public void greet() {  
        System.out.println("Hello I am a Bean");  
    }  
}
```

Greeter will be our bean and we will then try to add it in application context and use it in our application. Add createGretter method to the Runner.java which we create before. Important thing here to notice is the annotation Bean which tells us that method will give us a Bean.

```
package app;  
  
import org.springframework.boot.CommandLineRunner;  
import org.springframework.context.annotation.Bean;  
import org.springframework.stereotype.Component;  
  
@Component  
public class Runner implements CommandLineRunner {  
  
    @Override  
    public void run(String... args) throws Exception {  
        System.out.println("Hello World!");  
    }  
  
    @Bean  
    public Greeter createGreeter() {  
        return new Greeter();  
    }  
}
```

Now how do we access this bean in our application. We will create an instance of type Greeter where we want to use it with Autowired annotation. The autowired annotation should connect the instance with its bean and you will be able to use the bean in different places with this instance. 

```
package app;  
  
import org.springframework.beans.factory.annotation.Autowired;  
import org.springframework.boot.CommandLineRunner;  
import org.springframework.context.annotation.Bean;  
import org.springframework.stereotype.Component;  
  
@Component  
public class Runner implements CommandLineRunner {  
  
    @Autowired  
    private Greeter greeter;  
  
    @Override  
    public void run(String... args) throws Exception {  
        greeter.greet();  
    }  
  
}
```

This way of creating classes is much elegant and less messy than using singleton objects.

### Components

Now we will look into the better way of creating beans. Instead of explicitly creating method which return the instance of the bean like how we did in Greeter class above,  we can just use the annotation Component and remove the bean method.

Everything remains same, you can just remove the method bean. This tell us that components are just basically beans (Have to learn more about this concept).

```
package app;  
  
import org.springframework.context.annotation.Bean;  
import org.springframework.stereotype.Component;  
  
@Component  
public class Greeter {  
  
    public void greet() {  
        System.out.println("Hello I am a Bean");  
    }  
  
    public void TestBean() {  
        System.out.println("This is another instance of Greet bean");  
    }  
}
```

### Bean Configuration

There is also a third way of creating a bean. By using configuration annotation. One big advantage of creating beans by Bean annotation is that because we are returning the new instance of the class using constructor, we can pass different parameters to it. This can be really helpful. Using configuration we can achieve this and have multiple beans creating together.

Create a new class called Config with Configuration annotation and then add Bean annotation method to it.

```
package app;  
  
import org.springframework.context.annotation.Bean;  
import org.springframework.context.annotation.Configuration;  
  
@Configuration  
public class Config {  
    @Bean  
    public Greeter configureGreeter() {  
        return new Greeter();  
    }  
}
```

we can now remove the component annotation from the Greeter class since we are creating its bean in the configuration.

```
package app;  
  
public class Greeter {  
  
    public void greet() {  
        System.out.println("Hello I am a Bean");  
    }  
  
    public void TestBean() {  
        System.out.println("This is another instance of Greet bean");  
    }  
}
```

### Summary of Bean Creation

So until now we have seen total three ways of creating beans:

1. By Bean annotation - Create a method with @Bean annotation which return the new instance of the class
2. By Component annotation - we can just add @Component annotation on a class which will create a Bean for us
3. By Configuration annotation - We can have all our beans together. We create a class with @Configuration and then add all our bean methods with @Bean configuration there.



