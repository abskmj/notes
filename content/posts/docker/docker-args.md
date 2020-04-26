---
title: "Pass Parameters to Docker Build"
date: 2020-04-26T22:51:06+05:30
tags: ['Docker', 'ARG', 'CI']
---

# ARG in Dockerfile
> The `ARG` instruction defines a variable that users can pass at build-time to the builder with the docker build command using the `--build-arg <varname>=<value>` flag. More details at [docs.docker.com](https://docs.docker.com/engine/reference/builder/#arg)

## Example
Dockerfile
```
FROM debian:stable-slim

ARG HUGO_VERSION

LABEL maintainer "abskmj@gmail.com"
LABEL hugo.version ${HUGO_VERSION}
```

Pass the argument value
```bash
docker build -t hugo --build-arg HUGO_VERSION=0.69.0 .
```