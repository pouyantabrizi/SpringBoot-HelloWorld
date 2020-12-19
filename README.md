# SpringBoot-HelloWorld

Hi, I want to help you here with the simplest methods to pay attention only to the main content so that you can develop Spring Boot projects everywhere with Gradle build tools, without IDEs.

## Lessons:
   - [Lesson-1](#lesson-one)

<h2 id="lesson-one">Lesson 1</h2>
In this lesson we will talk about spring boot and directory

### What is the Spring boot?

Spring Boot is a Spring framework module which provides RAD (Rapid Application Development) feature to the Spring framework.
Spring Boot makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run".

### Learn What You Can Do with Spring Boot

Spring Boot offers a fast way to build applications. It looks at your classpath and at the beans you have configured, makes reasonable assumptions about what you are missing, and adds those items. With Spring Boot, you can focus more on business features and less on infrastructure.

### Set up the project

First you set up a Java project for Gradle to build. To keep the focus on Gradle, make the project as simple as possible for now.

###### Create the directory structure
In a project directory of your choosing, create the following subdirectory structure; for example, with *mkdir -p src/main/java/com/mycompany/hello*
*src/main/java* is a base directory for java and spring projects and ../com/mycompany/hello directory is a project custom directory that you can use any custom name for your project. Notice: don't change *src/main/java*  any way

└── src
    └── main
        └── java
            └── *** (Custom, You must have at least one package)
            
*Don't use the “default” Package*
When a class does not include a package declaration, it is considered to be in the “default package”. The use of the “default package” is generally discouraged and should be avoided. It can cause particular problems for Spring Boot applications that use the @ComponentScan, @EntityScan, or @SpringBootApplication annotations since every class from every jar is read.





