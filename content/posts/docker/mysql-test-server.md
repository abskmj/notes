---
title: "Start a test MySQL database using Docker"
date: 2021-05-31T10:35:00+05:30
tags: ["Docker","MySQL","Database"]
summary: " "
---

> Uses the official [docker images](https://hub.docker.com/_/mysql) from MySQL team 

# Steps
- Start the database server
```bash
docker run --rm --name=mysql -e MYSQL_ROOT_PASSWORD=<secret> -e MYSQL_DATABASE=<database_name> -p 3306:3306 -d mysql:latest

# example
docker run --rm --name=mysql -e MYSQL_ROOT_PASSWORD=change-me-later -e MYSQL_DATABASE=test -p 3306:3306 -d mysql:latest
```
- Options
```bash
docker run
 --rm # remove container when exits
 --name=mysql # name of the container
 -e MYSQL_ROOT_PASSWORD=<secret> # set the database password
 -e MYSQL_DATABASE=<database_name> # set the database name
 -p 3306:3306  # port forward 
 -v $PWD/db/:/docker-entrypoint-initdb.d/ # volume mount database init scripts
 -d mysql:latest # use latest version of the image
```
- View the logs
```bash
docker logs mysql
```

- Stop the database server
```bash
docker stop mysql
```