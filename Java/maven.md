## Basics

Maven is a java build tool. Like how npm is for JavaScript, Maven is for Java.
*  Maven uses a **Project Object Model (POM)** to manage a project. pom.xml is used as configuration file.


Generate a new maven project by scratch
```
mvn archetype: generate
```


## what is a pom

* The POM tells Maven what sort of project it is dealing with and how to modify default behavior to generate output from source.

### Super POM

* All Maven project POMs extend the Super POM, which defines a set of defaults shared by all projects. This Super POM is a part of the Maven installation.
* An analogy to how the Super POM is the parent for all Maven POM files, would be how `java.lang.Object` is the top of the class hierarchy for all Java classes.
* The Super POM defines some standard configuration variables that are inherited by all projects.

### Simplest POM

* All Maven POMs inherit defaults from the Super POM
* Such a simple POM would be more than adequate for a simple project—e.g., a Java library that produces a JAR file. It isn’t related to any other projects, it has no dependencies, and it lacks basic information such as a name and a URL. If you were to create this file and then create the subdirectory _src/main/java_ with some source code, running `mvn package` would produce a JAR in _target/simple-project-1.jar_.

### Effective POM

It is the merge between `The Super POM` and the _POM_ from `The Simplest POM`.


## Project dependencies

* Maven can manage both internal and external dependencies. 
* An external dependency for a Java project might be a library such as Plexus, the Spring Framework, or Log4J. An internal dependency is illustrated by a web application project depending on another project that contains service classes, model objects, or persistence logic.

### Transitive Dependencies

 * `project-a` depends on `project-b`, which in turn depends on `project-c`, then `project-c` is considered a transitive dependency of `project-a`.
 * Part of Maven’s appeal is that it can manage transitive dependencies and shield the developer from having to keep track of all of the dependencies required to compile and run an application.
 * Maven accomplishes this by building a graph of dependencies and dealing with any conflicts and overlaps that might occur. 
 * For example, if Maven sees that two projects depend on the same `groupId` and `artifactId`, it will sort out which dependency to use automatically, always favoring the more recent version of a dependency. Although this sounds convenient, there are some edge cases where transitive dependencies can cause some configuration issues. For these scenarios, you can use a dependency exclusion.

#### Conflict Resolution

There will be times when you need to exclude a transitive dependency, such as when you are depending on a project that depends on another project, but you would like to either exclude the dependency altogether or replace the transitive dependency with another dependency that provides the same functionality.

```
<dependencies>
    <dependency>
        <groupId>org.hibernate</groupId>
        <artifactId>hibernate</artifactId>
        <version>3.2.5.ga</version>
        // remove this dependency
        <exclusions>
            <exclusion>
                <groupId>javax.transaction</groupId>
                <artifactId>jta</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
    // include this, which is just doing the same job of javax.transaction
    <dependency>
        <groupId>org.apache.geronimo.specs</groupId>
        <artifactId>geronimo-jta_1.1_spec</artifactId>
        <version>1.1</version>
    </dependency>
</dependencies>
```

### what are maven coordinates

groupId = root package name / project name / UID of group that owns the project
artifactId = name of the package / name of final compilation unit
packaging = how you want the library to be packaged: .war, .jar, .ear etc? 
* LEARN: what is the difference between these java package versions?
version = what is the version of the package
* NOTE: snapshot indicates work in progress



It lets you create a hierarchy of dependencies. Parent dependencies can be used in child dependencies and then external dependencies can be exported. Only thing you have to do is to mention the dependencies in the pom.xml

## Life Cycles

A lifecycle is a collection of related activities pertaining to a specific type of build-management.

###  Standard lifecycles

- **clean** – Intended for clean-up of any prior build-managed outputs and artifacts.
- **default (build)** – Intended for project build, test and deployment of artifacts.
- **site** – Intended for project site documentation.


## sources

[1] https://youtu.be/KNGQ9JBQWhQ?si=V5MaCsx_ughmV3zX
[2] https://cguntur.me/2020/05/20/understanding-apache-maven-the-series/
[3] https://books.sonatype.com/mvnref-book/reference/index.html

[[1. Java Index | Index]]

