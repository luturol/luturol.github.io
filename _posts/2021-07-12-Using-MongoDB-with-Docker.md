---
layout: post
title: Using MongoDB with Docker
date:   2021-07-12 18:19:00
categories: 
- docker
- mongodb
---

# Using MongoDB with Docker

What you need to have installed:

 - Docker

> With you want to learn more about Docker, you can check my blog post about it by [clicking here](https://luturol.github.io/docker/Docker-101)

## Downloading [MongoDB Image](https://hub.docker.com/_/mongo)

```docker
docker image pull mongo
```

## Run a container

```docker
docker run -e MONGO_INITDB_ROOT_USERNAME=root -e MONGO_INITDB_ROOT_PASSWORD=root -p 27017:27017 mongo
```

**Change password and username for a suitable for you**

### What this command does

It will initialize your container and show you the logs while is initializing, so you can track if some errors appears in the cosole log.

**-e** will add **MONGO_INITDB_ROOT_USERNAME** enviroment variable with the value **root**. With that, your username to connect will be root.

**-e** will add **MONGO_INITDB_ROOT_PASSWORD** enviroment variable with the value **root**. With that, your pawword to connect will be root.

**-p** will share your local port with the port of the container. 27017 is port that mongodb use.

## Executing the same mongodb container after ended

1. You need to get the container ID from your mongodb container.

    ```docker
    docker container ps -a
    ```

1. With the container Id, now you can enter using the following command:

    ```docker
    docker start containerId
    ```
    
    It will enter inside the container with a bash terminal executing.

## Testin your connection
1. Testing your connection

    You must have some program to connect with MongoDB. You can use or [Mongo Compass](https://www.mongodb.com/pt-br/products/compass) or [Robot3](https://robomongo.org/) or the one you prefer.

    To connect you will need a connection string.

    ```
    mongodb://root:root@localhost:27017/admin
    ```

    This is the connection string to connect inside mongodb of our container.

## What does that connection string means:

1. First **root** is the username (if you changed, you must change in the connection string as well)

1. Second **root** is our password (if you changed, you must change in the connection string as well)

1. After @ is the IP you are trying to connect and the database that holds your user.

## References

- [MongoDB docker image](https://hub.docker.com/_/mongo)
- [MongoDb Docker do Balta.io](https://balta.io/blog/mongodb-docker)
- [Connection String URI Format from MongoDB Documentation](https://docs.mongodb.com/manual/reference/connection-string/)
