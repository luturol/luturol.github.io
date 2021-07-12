---
layout: post
title: Using MySQL with Docker
date:   2021-06-13 18:19:00
categories: 
- docker
- mysql
---

# Using MySQL with Docker

What you need to have installed:

 - Docker

> With you want to learn more about Docker, you can check my blog post about it by [clicking here](https://luturol.github.io/docker/Docker-101)

## Downloading [MySQL Image](https://hub.docker.com/_/mysql)

```docker
docker image pull mysql:5.7
```

## Run a container

```docker
docker run -e MYSQL_ALLOW_EMPTY_PASSWORD=yes -v folderForVolume:/var/lib/mysql mysql:5.7
```

**Change folderForVolume for a path from a folder to create the volume**.

### What this command does

It will initialize your container and show you the logs while is initializing, so you can track if some errors appears in the cosole log.

**-e** will add MYSQL_ALLOW_EMPTY_PASSWORD enviroment variable with the value **yes**. With that, you can enter in mysql without password.

**-v** will create a volume with the container to share some data between your pc and the container. With this, you will be able to create another container with the same data without losing any tables or queries. 

## Entering the container

1. You need to get the container ID from your mysql container.

    ```docker
    docker container ls
    ```

1. With the container Id, now you can enter using the following command:

    ```docker
    docker exec -it containerID bash
    ```
    
    It will enter inside the container with a bash terminal executing.

1. Enter MySQL

    ```bash
    mysql
    ```

    If it works, then will show in the console that you are inside the mysql. To test just execute a ```show databases``` to check.

## References

1. [MySQL docker image](https://hub.docker.com/_/mysql)
1. [Como rodar MySQL com Docker?](https://www.youtube.com/watch?v=S9BbUxmFaQI&ab_channel=AluraCursosOnline)

