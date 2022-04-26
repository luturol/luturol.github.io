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

## How to configure

### Requirements

1. Java SDK installed

    To verify with you have Java SDK installed just open terminal and execute the follow script:
    
    ```bash
    java --version
    ```
    
    If it shows java versions installed, then you are good to go (check if it is java 11+). If not then, you need to [download Java SDK](https://www.oracle.com/java/technologies/downloads/).

1. Go to [Spring Boot Initializer](https://start.spring.io/) to download de base project

    Spring has a site that you can download a Base Project with Spring configured on it. In this site, you can choose all base configurations you need in your project as such language (java, kotlin or groovy), dependencies, java version of your project and more...

1. Maven or Gradle

    If you choose on or another then you must have configured them on your computer. Maven has a wrapper that comes with the SpringBoot project already.