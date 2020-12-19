# SpringBoot-HelloWorld

Hi, I want to help you here with the simplest methods to pay attention only to the main content so that you can develop Spring Boot projects everywhere with Gradle build tools, without IDEs.
*This tutorial is a summary of the main Spring.io site tutorial and some other resources*

## Lessons:
   - [Lesson-1: What is the Spring Boot?](#lesson-one)
   - [Lesson-2: Create the project](#lesson-two)
   - [Lesson-3: Install Gradle to build the project](#lesson-three)

<h2 id="lesson-one">Lesson 1</h2>
In this lesson we will talk about spring boot

### What is the Spring boot?

Spring Boot is a Spring framework module which provides RAD (Rapid Application Development) feature to the Spring framework.
Spring Boot makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run".

### Learn What You Can Do with Spring Boot

Spring Boot offers a fast way to build applications. It looks at your classpath and at the beans you have configured, makes reasonable assumptions about what you are missing, and adds those items. With Spring Boot, you can focus more on business features and less on infrastructure.

<h2 id="lesson-two">Lesson 2</h2>
In this lesson we will create a new project in current directory

### Set up the project
First you set up a Java project for Gradle to build. To keep the focus on Gradle, make the project as simple as possible for now.

### Create the directory structure
In a project directory of your choosing, create the following subdirectory structure; for example, with **mkdir -p src/main/java/com/mycompany/hello**
**src/main/java** is a base directory for java and spring projects and **../com/mycompany/hello** directory is a project custom directory that you can use any custom name for your project. Notice: don't change **src/main/java**  any way
```
└── src
    └── main
        └── java
            └── *** (Custom, You must have at least one package)
```
**Don't use the “default” Package**
When a class does not include a package declaration, it is considered to be in the “default package”. The use of the “default package” is generally discouraged and should be avoided. It can cause particular problems for Spring Boot applications that use the @ComponentScan, @EntityScan, or @SpringBootApplication annotations since every class from every jar is read.

### Create java classes in your project 
```
└── src
    └── main
        └── java
            └── com
               └── mycompany
                  └── hello
                     └── HelloWorld.java
                     └── Greeter.java
```
HelloWorld.java:
```java
package com.mycompany.hello;

public class HelloWorld {
  public static void main(String[] args) {
  Greeter greeter = new Greeter();
  System.out.println(greeter.sayHello());
  }
}
```
Greeter.java:
```java
package com.mycompany.hello;

public class Greeter {
  public String sayHello() {
  return "Hello world!";
  }
}
```

<h2 id="lesson-three">Lesson 3</h2>
In this lesson we will install Gradle build tools to build our first project

### Install Gradle
Go ahead to [Gradle install](https://gradle.org/install/) and install gradle on your operating system(OS), make sure your installation is correct, after that run **gradle -v** to see your gradle version

Now that Gradle is installed, see what it can do. Before you even create a build.gradle file for the project, you can ask it what tasks are available:

gradle tasks
You should see a list of available tasks.

### Build Java Code
Starting simple, create a very basic *build.gradle* file in the <project folder>(*../com/mycompany/hello) you created at the beginning of this guide. Give it just just one line:

```apply plugin: 'java'```

This single line in the build configuration brings a significant amount of power. Run gradle tasks again, and you see new tasks added to the list, including tasks for building the project, creating JavaDoc, and running tests.

You’ll use the gradle build task frequently. This task compiles, tests, and assembles the code into a JAR file. You can run it like this:

```gradle build```

After a few seconds, "BUILD SUCCESSFUL" indicates that the build has completed.

To see the results of the build effort, take a look in the build folder. Therein you’ll find several directories, including these three notable folders:

**classes. The project’s compiled .class files.**

**reports. Reports produced by the build (such as test reports).**

**libs. Assembled project libraries (usually JAR and/or WAR files).**

The classes folder has .class files that are generated from compiling the Java code. Specifically, you should find HelloWorld.class and Greeter.class.
At this point, the project doesn’t have any library dependencies, so there’s nothing in the dependency_cache folder.
The reports folder should contain a report of running unit tests on the project. Because the project doesn’t yet have any unit tests, that report will be uninteresting.

The libs folder should contain a JAR file that is named after the project’s folder. Further down, you’ll see how you can specify the name of the JAR and its version.

                     
                     





