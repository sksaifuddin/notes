This page will have all the notes I take while doing a spring course by Marco Behler.

## Java Webapps without Spring

We will first try to create a small webapp without using Spring. This will teach us what problem exactly does the spring solves and also learn its basics.

### Project Setup

setup a basic maven project. We create a project folder and then keep a pom.xml inside. Few things to know in pom.xml
* GroupId = Project domain name
* artifactId = actual name of the project
* snapshot = work in progress

Packaging: It can have jar and war. Historically, the packaging for web applications would have been `_<packaging>war</packaging>_` . You would take the resulting war-file and put it into a servlet container like [Tomcat](http://tomcat.apache.org/) to run your web application [2].

Lately, frameworks like Spring Boot will pre-configure Maven to produce so called "fat jar" files. They are called fat, because those .jar files include Tomcat and all other 3rd party libraries, all in one file.

Check if everything is right in pom.xml
```
mvn validate
```

### Rendering HTML pages

We will first render a simple web page with HttpServlets (Spring internally uses this). You will need two things for that:
1. A servlet container, something that can "run" servlets and make them available whenever you open up your browser and go to [http://localhost:8080](http://localhost:8080/). Popular servlet containers in Java are [Tomcat](http://tomcat.apache.org/) or [Jetty](https://www.eclipse.org/jetty/). [2]
2. The HttpServlet, containing the code to display HTML pages, itself. [2]

==Learn more: [[Servlet API]] and [[HttpServlets]] and how the architecture works==

Previously, we had to package the code to war file and then copy it in the tomcat directory and then start it. But with jar file we can have embedded tomcat which will be inside jar file which will run the servlet (💡interesting, this look like what we did in PHP, download xamp and run php code)

Add embedded tomcat dependency in pom.xml. We will the create a class extending HttpServlet class and then add html code to it.  Just creating a servlet class is not enough, just like in node.js we have to create its server and then gives routes and then register the servlet class. This can be done in another class called ApplicationLauncher which will have main method. If you run this class from IDE and go to localhost:8080, it should work.

We will now try to package this servlet in jar and try to run it directly the way spring boot does it. To start packaging just do mvn package. This will create a jar file in your target folder with the name you provided in the pom.xml, but when you try to run this jar file with the command: java -jar target\myfancypdfinvoices-1.0-SNAPSHOT.jar you will get below error message:

```
no main manifest attribute, in target\myfancypdfinvoices-1.0-SNAPSHOT.jar
```

Its a complicated way of saying that Java does not know which class to run inside the jar file. It should run ApplicationLauncher class, but for that we need maven to create a manifest file and put it inside the jar file which will have this required information.

To add the manifest file inside maven you have to add another dependency called maven-jar-plugin and add configuration with manifest and main class as ApplicationLauncher. something liek this:

```
<configuration> <archive> <manifest> <mainClass>com.marcobehler.ApplicationLauncher</mainClass> </manifest> </archive> </configuration>
```

now if you try to build again using package command to run, there will another error:
```
Error: Unable to initialize main class com.marcobehler.ApplicationLauncher Caused by: java.lang.NoClassDefFoundError: jakarta/servlet/Servlet
```

When you build a .jar file, Maven will, by default, only put _your own_ source code into that .jar file. It will _not_ put the external libraries your project depends on inside that .jar file [2]. To remove this error we need another plugin called shade. We have to do configuration of shade plugin and then build - run again. Now it will work.

This whole process of adding the manifest, and then shading, is done by Spring boot in its own way. this is reason we never had to do it ourselves, although we ran lot of spring boot applications.

Sources:
1. A short guide to maven - https://www.marcobehler.com/guides/mvn-clean-install-a-short-guide-to-maven
2. Confident Spring Professional course