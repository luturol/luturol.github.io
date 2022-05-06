---
layout: post
title: How to start a Spring Boot Project
date:   2022-04-26 18:19:00
categories: 
- java
- springboot
---

# How to start a Spring Boot Project

In this article I will show you how to start a Spring Boot project. The porpouse of this article is to show you how to configure, start and execute a simple spring boot project from basics.

Why am I doing this? Because curently I'm changing projects and the new project will use Java as the main Tech and now I need to learn more about Java and it's frameworks.

## What is Spring Boot

Is a framework 

## How to configure

1. Go to [Spring Boot Initializer](https://start.spring.io/) to download de base project

    Spring has a site that you can download a Base Project with Spring configured on it. In this site, you can choose all base configurations you need in your project as such language (java, kotlin or groovy), dependencies, java version of your project and more...

1. Open your project inside your IDE and you are good to go

### Requirements

1. Java SDK installed

    To verify with you have Java SDK installed just open terminal and execute the follow script:
    
    ```bash
    java --version
    ```
    
    If it shows java versions installed, then you are good to go (check if it is java 11+). If not then, you need to [download Java SDK](https://www.oracle.com/java/technologies/downloads/).

1. Maven or Gradle

    If you choose on or another then you must have configured them on your computer. Maven has a wrapper that comes with the SpringBoot project already.

## Create your first Controller and Endpoint

To create your Controller you need to add a class in the same folder or bellow the folder from your Application class. If you create above Application class, Spring will not recognize your class.

When you add your class, you must add one of those two annotations on it: ```@Controller``` or ```@RestController```.

```@Controller``` you must specify in all methods that you want to return a response body (add ```@ResponseBody``` annotation) to it. If you don't then, it will assume that you are trying to return a value to a JSP or Thymeleaf page.

```@RestController``` you don't need to add ```@ResponseBody``` annotation to methods that return a response body. It already assumes that the method will return a body.

Your class will be something like this:

```java
@RestController
public class MangaController {

    @RequestMapping("/mangas")
    public List<String> lista(){
        return Arrays.asList("Solo Leveling", "The Legend of the Northern Blade", "Tales of Demons and Gods");
    }
}
```

Using ```@RestController``` you can add the request mapping to the MangaController class declaration so you does not need to add in every endpoint you built. 

```java
@RestController
@RequestMapping("/mangas")
public class MangaController {

    @GetMapping
    public List<String> list(){
        return Arrays.asList("Solo Leveling", "The Legend of the Northern Blade", "Tales of Demons and Gods");
    }
}
```

In your endpoints you will need yo specify which verb will use yo access. Just add one of this annotations to it.

```java
@GetMapping
@PostMapping
@PutMapping
@DeleteMapping
@PatchMapping
```

Now you have your endpoint and controller. 

Run your project and try access through ```localhost:8080/mangas``` to check the mangas list reponse. 

And that's it.

Don't forget to eat clean and drink water.

Peace!!