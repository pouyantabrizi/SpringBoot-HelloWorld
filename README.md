# SpringBoot-HelloWorld

Hi, I want to help you here with the simplest methods to pay attention only to the main content so that you can develop Spring Boot projects everywhere with Gradle build tools, without IDEs.

**This tutorial is a summary of the main Spring.io site tutorial and some other resources**

## Lessons:
   - [Lesson-1: What is the Spring Boot?](#lesson-one)
   - [Lesson-2: Create the project](#lesson-two)
   - [Lesson-3: Install Gradle to build the project](#lesson-three)
   - [Lesson-4: Declare dependencies in gradle.build file](#lesson-four)

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
Starting simple, create a very basic *build.gradle* file in the <project folder> you created at the beginning of this guide. Give it just just one line:
   
```
└── src
└── build.gradle
```
   
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

<h2 id="lesson-four">Lesson 4</h2>
In this lesson we will declare dependencies in gradle.build file

### Declare dependencies
The simple Hello World sample is completely self-contained and does not depend on any additional libraries. Most applications, however, depend on external libraries to handle common and/or complex functionality.

For example, suppose that in addition to saying "Hello World!", you want the application to print the current date and time. You could use the date and time facilities in the native Java libraries, but you can make things more interesting by using the Joda Time libraries.

First, change **HelloWorld.java** to look like this:

```java
package com.mycompany.hello;

import org.joda.time.LocalTime;

public class HelloWorld {
  public static void main(String[] args) {
    LocalTime currentTime = new LocalTime();
    System.out.println("The current local time is: " + currentTime);

    Greeter greeter = new Greeter();
    System.out.println(greeter.sayHello());
  }
}
```

Here HelloWorld uses **Joda Time’s LocalTime class** to get and print the current time.

If you ran gradle build to build the project now, the build would fail because you have not declared Joda Time as a compile dependency in the build.

For starters, you need to add a source for 3rd party libraries.(Add to build.gradle file)
```
repositories {
    mavenCentral()
}
```

The repositories block indicates that the build should resolve its dependencies from the Maven Central repository. Gradle leans heavily on many conventions and facilities established by the Maven build tool, including the option of using Maven Central as a source of library dependencies.

Now that we’re ready for 3rd party libraries, let’s declare some.(Add to build.gradle file)
```
sourceCompatibility = 1.8
targetCompatibility = 1.8

dependencies {
    implementation "joda-time:joda-time:2.2"
    testImplementation "junit:junit:4.12"
}
```

With the dependencies block, you declare a single dependency for Joda Time. Specifically, you’re asking for (reading right to left) version 2.2 of the joda-time library, in the joda-time group.

Another thing to note about this dependency is that it is a compile dependency, indicating that it should be available during compile-time (and if you were building a WAR file, included in the /WEB-INF/libs folder of the WAR). Other notable types of dependencies include:

implementation. Required dependencies for compiling the project code, but that will be provided at runtime by a container running the code (for example, the Java Servlet API).

testImplementation. Dependencies used for compiling and running tests, but not required for building or running the project’s runtime code.

Finally, let’s specify the name for our JAR artifact.
```
jar {
    archiveBaseName = 'gs-gradle'
    archiveVersion =  '0.1.0'
}
```
Now run **gradle build** again
At this stage, you will have built your code. You can see the results here:

```
build
├── classes
│   └── main
│       └── hello
│           ├── Greeter.class
│           └── HelloWorld.class
├── dependency-cache
├── libs
│   └── gs-gradle-0.1.0.jar
└── tmp
    └── jar
        └── MANIFEST.MF
```
Included are the two expected class files for Greeter and HelloWorld, as well as a JAR file. Take a quick peek:
```
$ jar tvf build/libs/gs-gradle-0.1.0.jar

  0 Fri May 30 16:02:32 CDT 2014 META-INF/
 25 Fri May 30 16:02:32 CDT 2014 META-INF/MANIFEST.MF
  0 Fri May 30 16:02:32 CDT 2014 hello/
369 Fri May 30 16:02:32 CDT 2014 hello/Greeter.class
988 Fri May 30 16:02:32 CDT 2014 hello/HelloWorld.class
```
The class files are bundled up. It’s important to note, that even though you declared joda-time as a dependency, the library isn’t included here. And the JAR file isn’t runnable either.

To make this code runnable, we can use gradle’s application plugin. Add this to your build.gradle file.
```
apply plugin: 'application'

mainClassName = 'hello.HelloWorld'
```
Then you can run the app!
```
$ gradle run

:compileJava UP-TO-DATE
:processResources UP-TO-DATE
:classes UP-TO-DATE
:run
The current local time is: 16:16:20.544
Hello world!

BUILD SUCCESSFUL

Total time: 3.798 secs
```

To wrap things up for this guide, here is the completed build.gradle file:
```
build.gradle

apply plugin: 'java'
apply plugin: 'eclipse'
apply plugin: 'application'

mainClassName = 'hello.HelloWorld'

// tag::repositories[]
repositories {
    mavenCentral()
}
// end::repositories[]

// tag::jar[]
jar {
    archiveBaseName = 'gs-gradle'
    archiveVersion =  '0.1.0'
}
// end::jar[]

// tag::dependencies[]
sourceCompatibility = 1.8
targetCompatibility = 1.8

dependencies {
    implementation "joda-time:joda-time:2.2"
    testImplementation "junit:junit:4.12"
}
// end::dependencies[]
// tag::wrapper[]
// end::wrapper[]
```

**Congratulations! You have now created a simple yet effective Gradle build file for building Java projects.**



