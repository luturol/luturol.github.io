---
layout: post
title: How to use Maven
date:   2022-05-10 18:19:00
categories: 
- java
- maven
---

# What is [Maven](https://maven.apache.org/)

Is a project manager tool to help you build your application and manage dependencies.

## How to install

To install on linux:

```bash
sudo apt update
sudo apt install maven
```

check if maven is installed:

```bash
mvn -version
```

## How to create a Maven project

Just create a normal project and select Maven option.

You need to be careful about a few things: ```groupId```, ```archetype``` and ```artifactId```.

### Group Id

It's the company name with org. or com. prefixes. It will create folders with the correspond GroupId value.

### Archetype

It's the configuration to set to create other types of project. It will configure your project to it.

Example:

If you want to create a jira plugin, then select the jira-plugin-archetype. ]

By default, it does not use one.


### Artifact Id

It's the name of the project. It will appear in the JAR file or WAR file when build your application.


### Project Structure

```
ProjectName
    - src
        - main
            - java
                - com
                    - organization                       
            - resources
        - test
            - java
            - resources
    - pom.xml
```

pom.xml is the maven configuration file. It contains the dependencies and other configs.


## How to add Dependencies in your project

Inside ```pom.xml``` add inside the ```<project></project>``` tag add the tag ```<dependencies></dependencies>```.

In dependencies tag you will add your dependencies. How? just like this:

1. Add another tag called ```<dependency></dependency>```

1. Add the group id and artifact id of your dependency

    Example:
    ```xml
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
        </dependency>
    </dependencies>
    ```

1. You can add the version of the dependency

    Example:
    ```xml
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
    </dependencies>
    ```

1. You can add the [scope tag](https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html#Dependency_Scope) to set how the dependency will be used.

    compile, provided, runtime, system, test
    Example:
    ```xml
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
    ```

You need to save your project and download dependencies after that.


## How to add remote repository

It's common for companies to have their own dependency repository to storage their own package. So, to add their remote repository to your pom.xml for maven download their packages you just need to add two tags: ```<repositories></repositories>``` and ```<repository></repository>```.

Example:

```xml
<repositories>
    <repository>
        <id>spring-repo</id>
        <url>https://repo.spring.io/release</url>
    </repository>
</repositories>
```

Now maven will search for this repository to download dependencies.

Inside url tag you can add a folder or a private url, or an IP to an internal server...

## How to build your maven application

To compile your project:

```bash
mvn compile
```

To clean target folder:

```bash
mvn clean
```

If it result on a error saying that you are using the wrong JAVA version, then you need to configure the default JAVA version to use on your project.

```xml
<build>
    <plugins>
        <plugin>
            <artifactId>maven.compiler-plugin</artifactId>
            <configuration>
                <source>11</source>
                <target>11</target>
            </configuration>
        </plugin>
    </plugins>
</build>
```

Everything that is related to build, you set inside the ```build``` tag on ```pom.xml```

You can run ```mvn test``` to execute tests from your application.

## How to generate a package

Maven has a command to create the package, aka build, of your application.

```bash
mvn package
```

This command will check inside ```pom.xml``` to verify what type of file will be created, if it's a JAR or a WAR.

This file will be stored inside the ```target/``` folder.

To configure the packaging type just add the tag ```packaging``` in ```pom.xml```

Example:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.spring-boot-react</groupId>
	<artifactId>demo</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

    //other configs
    // ...
</project>
```

## How to install your application

You can use this command to install your application

```bash
mvn install
```

This will make a build, package and install in your local computer.

## How to deploy your application in a local or remote repository

```bash
mvn deploy
```

To use this you need to configure local repository inside the ```repositories``` tag in the ```pom.xml```
