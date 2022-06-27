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