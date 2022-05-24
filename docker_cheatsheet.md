# Docker Cheatsheet

**DOCKERFILE**: builds an image given instructions (FROM, RUN, ...)

```dockerfile
    FROM - base img...you can have more than one FROM instruction in one Dockerfile.
    COPY vs ADD - prolly use COPY
    ENV - setting environment variables
    RUN - let’s run commands
    VOLUME - another source of confusion, what’s the difference between Dockerfile VOLUME and container volumes?
    USER - when root is too mainstream
    WORKDIR - set the working directory
    EXPOSE - get your ports right
    ONBUILD - give more flexibility to your team and clients
```

```sh
# build the image on your local machine names myimg
$ docker build -t myimg .

# launch a container
$ docker run -d myimg
```

**DOCKER-COMPOSE**: defines/runs multi-container Docker apps (services, ports, env vars, commands, ...)

```sh
$ docker-compose up/down start/stop pause/unpause ps
```

## Dockerfile

### Example - node
```dockerfile
FROM node:16
WORKDIR /usr/src/my-app-directory

# Install app dependencies
COPY package*.json ./

RUN npm install

# Bundle app source
COPY . .

EXPOSE 8080
CMD [ "node", "server.js" ]
```

### Example - ubuntu/python plain
```dockerfile
FROM ubuntu:latest
MAINTAINER john doe 

RUN apt-get update
RUN apt-get install -y python python-pip wget
RUN pip install Flask

ADD hello.py /home/hello.py

WORKDIR /home
```

## Docker Compose

```yml
version: '2'

services:
  web:
    # build from Dockerfile or image
    # image: ubuntu
    build:
      context: ./Path
      dockerfile: Dockerfile
    ports:
     - "5000:5000"
    volumes:
     - .:/code
  redis:
    image: redis
```
