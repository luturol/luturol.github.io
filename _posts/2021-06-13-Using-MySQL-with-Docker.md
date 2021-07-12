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

## Downloading MySQL Image

```docker
docker image pull mysql:5.7
```

## Run a container

```docker
docker run -e MYSQL_ALLOW_EMPTY_PASSWORD=yes -v folderForVolume:/var/lib/mysql mysql:5.7
```

**Change folderForVolume for a path from a folder to create the volume**.

## Entering the container

You need to get the container ID from your mysql container.
```docker
docker container ls
```

with the container Id, now you can enter using the following command:

```docker
docker exec -it containerID
```


## References

1. [https://www.youtube.com/watch?v=S9BbUxmFaQI&ab_channel=AluraCursosOnline](Como rodar MySQL com Docker?)
