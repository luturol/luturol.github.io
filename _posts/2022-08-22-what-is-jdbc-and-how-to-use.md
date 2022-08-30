---
layout: post
title: What is JDBC and how to use
date:   2022-08-22 18:19:00
categories: 
- java
---

# What is JDBC and how to use

In this article you will learn what is JDBC and how on your Java project. We will use Docker with PostgreSQL and Java 17 in this tutorial to explain and to execute it.

Repository of this article you can find by clicking [here](https://github.com/luturol/LearningJava).

## What is JDBC

JDBC is an acronym for Java Database Connectivity. It's an API made in Java to make connections to the database easier. You will use to access your database through your java application.

## How to use

You will need to download a JAR file with the JDBC implementation from the Database you are using. It will be the driver to connect with your Database.

From PostegreSQL you can download [here](https://jdbc.postgresql.org/download.html).

### Acessing Driver JAR

Add the external library in your project by searching for the External Library Button on your favorite IDE:
 - on [IntelliJ](https://stackoverflow.com/questions/1051640/correct-way-to-add-external-jars-lib-jar-to-an-intellij-idea-project).
 - on [Eclipse](https://stackoverflow.com/questions/2824515/how-to-add-external-library-properly-in-eclipse)

or you can call the driver on your class by using ```Class.forName("org.postgresql.Driver");``` change ```org.postgresql.Driver``` for your current driver.

### Using JDBC

To use JDBC we will need to create a new Java Project and start coding.

To connect to ours Database, we will need to use ```java.sql``` classes and implementations to help. First let's add a call to ```DriverManager.getConnection``` method and pass ours connection string to it.

```java
public Connection Create() throws SQLException {
    String jdbc = "jdbc:postgresql://localhost/postgres?user=java&password=java";

    return DriverManager.getConnection(jdbc);
}
```


# References

- [How to Add JAR file to Classpath in Java?](https://www.geeksforgeeks.org/how-to-add-jar-file-to-classpath-in-java/)
- [Using external libraries in Java](https://opensource.com/article/20/2/external-libraries-java)
- [Curso de Java e JDBC: trabalhando com um banco de dados](https://cursos.alura.com.br/course/jdbc-dao-persistencia)
- [O que É JDBC?](https://www.ibm.com/docs/pt-br/developer-for-zos/14.1.0?topic=support-what-is-jdbc)
- [JDBC tutorial](https://www.devmedia.com.br/jdbc-tutorial/6638)
- [PostgreSQL JDBC Driver](https://jdbc.postgresql.org/download.html)