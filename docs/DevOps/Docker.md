# Docker

Docker has been quite useful in developing and scaling applications in containers. It isolates the app from the infrastructure. A container is a running instance of an image.

## Getting Started

To install Docker there are a ton of methods you can find [here](https://docs.docker.com/get-docker/
). You can select your OS and then follow the instructions to install.

## Commands

Some commands that you can find useful -

1) **To test your Docker** - `docker run hello-word`
2) **To pull and image from Docker** - `docker pull debian`
3) **To run the image using interactive mode** - `docker run -t debian`
    
    *This command spins up a container with a unique id*
4) **To check all the containers** - `docker ps`

    *The above command is to get all the running containers. To get all containers dead and running you should* - `docker ps -a`

5) **To delete a container we use** - `docker rm <container id>`
6) **To get all images on your PC** - `docker images`
7) **To delete an image we use** - `docker rmi <image id>`
8) **To run a dead container in interactive mode** - `docker start -i <docker id>`
9) **Creating a custom image from a container** - `docker commit -m "my message" <container ID> <name of image>`

## Dockerfile
The Dockerfile is written to build a custom image. It consists of commands to build the image.

A quick example of a Dockerfile for node is -
```Dockerfile
FROM node
WORKDIR /app
COPY package.json /app
RUN npm install
COPY . /app
CMD ["npm", "start"]
```

After adding the Dockerfile to the root of your directory just use the command - `docker build -t mycustomtag .`

### Why tags are important?
They provide unique names assigned by the user to identify the custom images.

### Playing around
The custom image built can now be run in the interactive mode using the following command - `docker run -it -p 3000:3000 mycustomtag`

To run the custom image in detached mode we will use the following command - `docker run -d -p 3000:3000 mycustomtag`
    
*Detached mode means without a prompt or verbose*

*The 3000:3000 means exposing the docker containers internal port to the external port*

### Untested
A resource I found on YouTube states that one can use the automatic server restart in *nodemon* with Docker. I haven't tried it yet but it looks like a good idea!

Link to video - [Docker-izing a NodeJS ExpressJS API](https://www.youtube.com/watch?v=CsWoMpK3EtE)