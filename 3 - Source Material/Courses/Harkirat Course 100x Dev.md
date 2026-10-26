- https://flexboxfroggy.com/ (for learning/revising flex box)
- https://codepip.com/games/ (to learn css faster - should be really helpful)
- Tags -> 
- Attributes -> 
- Inline styles -> 
- Js Basics, data types, loops, ….
- External styles, classes, id -> 
- Flexbox -> 
- Connecting JS to HTML (selectors, DOM)  -> 
- Chrome dev tools -> 

HTML 
Find some cheatsheet for it as well ( not to worry about it )

CSS
 https://github.com/mayank190801/CSS_Syntax/blob/main/cheatsheet.txt
#### JavaScript
https://github.com/mayank190801/JavaScript_Syntax/blob/main/cheatsheet.js

#### JavaScript

Map , Filter , find and sort -> cool stuff 








### Docker

#####  Why to use docker??
- Kubernetes / container orchaestration requires docker understanding
- Running processes in isolated environments. (multiple benefits)
- Starting projects locally 
#### Containers
##### What are containers
- Containers are a way to package and distribute software applications in a way that makes them easy to deploy and run consistently across different environments. 
- They allow you to package an application, along with all its dependencies and libraries, into a single unit that can be run on any machine with a container runtime, such as Docker.
- run on any machine 
- run consistently across different environments 
##### Why need containers?? 
- Everyone has different Operating systems
- Steps to run a project can vary based on OS
- Extremely harder to keep track of dependencies as project grows
##### Benefits of containers
1. Let you describe your `configuration` in a single file
2. Can run in isolated environments
3. Makes Local setup of OS projects a breeze
4. Makes installing auxiliary services/DBs easy
5. For Reference, the following command starts `mongo` in all operating systems -
```javascript
docker run -d -p 27017:27017 mongo
```
6. Docker isn’t the only way to create containers

##### Inside Docker

![[Screenshot 2024-06-29 at 2.11.27 PM.png]]

###### 1. Docker Engine

Docker Engine is an open-source `containerization` technology that allows developers to package applications into `container`
Containers are standardized executable components combining application source code with the operating system (OS) libraries and dependencies required to run that code in any environment.

###### 2. Docker CLI

The command line interface lets you talk to the `docker engine` and lets you start/stop/list containers
```javascript
docker run -d -p 27017:27017 mongo
```
Docker cli is not the only way to talk to a docker engine. You can hit the docker `REST` API to do the same things

###### 3. Docker registry

The `docker registry` is how Docker makes money.
It is similar to `github`, but it lets you push `images` rather than `sourcecode`
Docker’s main registry - [https://dockerhub.com/](https://dockerhub.com/)
Mongo image on docker registry - [https://hub.docker.com/_/mongo](https://hub.docker.com/_/mongo)

##### Images Vs Containers

![[Screenshot 2024-06-29 at 2.17.17 PM.png]]

**Docker Image** 
- A Docker image is a lightweight, standalone, executable package that includes everything needed to run a piece of software, including the code, a runtime, libraries, environment variables, and config files.
- A good mental model for an image is `Your codebase on github`

**Docker Container**
- A container is a running instance of an image. It encapsulates the application or service and its dependencies, running in an isolated environment.
- A good mental model for a container is when you run `node index.js` on your machine from some source code you got from github

###### What mostly we do with docker??
- create an image and push it to docker
- start container locally using other peoples image (or your images)
- Deploy to Kubernetes or AWS machines 
##### Port Mapping

![[Screenshot 2024-06-29 at 2.28.00 PM.png]]

- I have to specially add the port mapping of my machine to this container port 
- **docker run -d -p 27018:27017 mongo**
- Transfer request from this port of my mac machine to this port of the container 

##### Docker Commands
- docker 
- docker run mongo 
- docker images (It will list all the images present)
- docker ps (It will list all the containers running)
- docker run -d mongo (Run the image in a container with detached mode, not in the same terminal)
- docker run -p 27018:27017 -d mongo  (Attaching a port to your container)
- docker kill :containerID (how to shut down an container)
- docker rmi :image --force (to delete the image from your machine)
- docker build -t backend-app . (-t :name helps you give a name to your image, '.' is for the current location)
- docker exec  (to execute an command inside the container)
- docker exec <container_name_or_id> ls /path/to/directory (list all files in the container)
- docker exec -it <container_name_or_id> /bin/bash  (interact with the container)
- docker volume create volume_database
- docker run -v volume_database:/data/db -p 27017:27017 mongo
- docker volume ls
- docker logs :containerId 
- 

##### Dockerfile (imp)

What is a dockerfile? 
- If you want to create an image from your own code, that you can push to `dockerhub`, you need to create a `Dockerfile` for your application.
- A Dockerfile is a text document that contains all the commands a user could call on the command line to create an image.

A dockerfile has 2 parts
1. Base image
2. Bunch of commands that you run on the base image (to install dependencies like Node.js)

 **Demo docker file** 
![[Screenshot 2024-06-29 at 3.12.46 PM.png]]

- `**WORKDIR**`: Sets the working directory for any `**RUN**`, `**CMD**`, `**ENTRYPOINT**`, `**COPY**`instructions that follow it.
- `**RUN**`: Executes any commands in a new layer on top of the current image and commits the results.
- `**CMD**`: Provides defaults for executing a container. There can only be one CMD instruction in a Dockerfile.
- `**EXPOSE**`: Informs Docker that the container listens on the specified network ports at runtime.
- `**ENV**`: Sets the environment variable.
- `**COPY**`: Allow files from the Docker host to be added to the Docker image

Simple Sober 
- **Anything present inside CMD will run when you start the container**
- **Where RUN command will run when you will build the image**
- .dockerignore - For not copying over node_module while using COPY command 

Q. How to SSH into those containers?? What are the ways for that?? It might be something you can learn from here 
###### How to pass env variables ???
- docker run -p 3000:3000 -e DATABASE_URL="postgres://avnadmin:<YOUR_AIVEN_PASSWORD>@pg-35339ab4-harkirat-d1b9.a.aivencloud.com:25579/defaultdb?sslmode=require" image_name (this might go inside .env file)
- Another way was also copying the env files while creating your image, locally we can use that method as well. ENV DATABASE_URL="lkasjdflasfdasdfj" (but not recommended, otherwise this will be present on github as well)

Pushing to dockerhub is not a difficult task - but there are steps which you can copy and have them here 

### What are Layers in Docker
- In Docker, layers are a fundamental part of the image architecture that allows Docker to be efficient, fast, and portable. A Docker image is essentially built up from a series of layers, each representing a set of differences from the previous layer.

![[Screenshot 2024-06-29 at 4.29.23 PM.png]]

**How layers are made -**

1. **Base Layer:** The starting point of an image, typically an operating system (OS) like Ubuntu, Alpine, or any other base image specified in a Dockerfile.
2. **Instruction Layers:** Each command in a Dockerfile creates a new layer in the image. These include instructions like `**RUN**`, `**COPY**`, which modify the filesystem by installing packages, copying files from the host to the container, or making other changes. Each of these modifications creates a new layer on top of the base layer.
3. **Reusable & Shareable:** Layers are cached and reusable across different images, which makes building and sharing images more efficient. If multiple images are built from the same base image or share common instructions, they can reuse the same layers, reducing storage space and speeding up image downloads and builds.
4. **Immutable:** Once a layer is created, it cannot be changed. If a change is made, Docker creates a new layer that captures the difference. This immutability is key to Docker's reliability and performance, as unchanged layers can be shared across images and containers.
![[Screenshot 2024-06-29 at 4.42.49 PM.png]]

1. Base image creates the first layer
2. Each `RUN`, `COPY` , `WORKDIR` command creates a new layer
3. Layers can get re-used across docker builds (notice `CACHED` in 1/6)
4. You can share layers across different builds 
### Thought experiment

How often in a project do you think `dependencies change` ?
How often does the `npm install` layer need to change?
Wouldn’t it be nice if we could `cache` the `npm install` step considering dependencies don’t change often?

We will discuss two dockefiles, and see the optimisation difference between them

![[Screenshot 2024-06-29 at 4.50.01 PM.png]]
- In the above Dockerfile, we can see that whenever any code changes , or any new dependency is added, the layer from 7,8,9 are also considered changed and now needs to re-run
- Should code changes in the project, impacts the npm install and rest of the commands, the answer is no! 

![[Screenshot 2024-06-29 at 4.51.57 PM.png]]
- In this above file, only if new dependencies are added to the codebase, the layer npm install and npx prisma generate will be updated!!! Otherwise incase of normal code source changes, till step 11 everything will be cached!! - hence optimised!

![[Screenshot 2024-06-29 at 4.56.46 PM.png]]

###  Networks and volumes

These are concepts that become important when you have multiple containers running in which you
1. Need to persist data across docker restarts
2. Need to allow containers to talk to each other

![[Screenshot 2024-06-29 at 5.10.51 PM.png]]

### Volumes

- If you restart a `mongo` docker container, you will notice that your data goes away.
- This is because docker containers are `transitory` (they don’t retain data across restarts)
- docker volume create volume_database
- docker run -v volume_database:/data/db -p 27017:27017 mongo
- Above here /data/db is the place where mongo actually stores the data, and hence that will change with different databases. 
- docker volume ls
- This way data will be persisted in some volumne and even you restart the container it will still be safe
### Network
 ![[Screenshot 2024-06-29 at 5.38.58 PM.png]]

- In Docker, a network is a powerful feature that allows containers to communicate with each other and with the outside world.
- Docker containers can’t talk to each other by default.
- [`localhost`](http://localhost/) on a docker container means `it's own network` and not the network of the `host machine`
- So basically previously when you used to call mongo db using localhost:27107, at that time your maching localhost was connected to the container port 27017, but when you call this from within a container then it won't work since now the network is different for the container. The localhost:27017 is inside of that container and not the machine one. 
##### How to make containers talk to each other?

- Attach them to the same network
- First build the image -> docker build -t image_tag .
- Create a network -> docker network create my_custom_network
- docker network ls 
- docker run -d -v volume_database:/data/db --name mongo --network my_custom_network -p 27017:27017 mongo
- After the above step is done, update the codebase in your node repo, now rather than localhost/27017 you should update to below stuff
![[Screenshot 2024-07-01 at 7.58.25 PM.png]]
- Now build your nodejs project again
- docker run -d -p 3000:3000 --name backend --network my_custom_network image_tag
- docker logs <container_id>

Good to know 
1. Try to visit an endpoint and ensure you are able to talk to the database
2. If you want, you can remove the port mapping for mongo since you don’t necessarily need it exposed on your machine
3. Basically both are attached to some similar network, hence no need to expose ports on our machine now. 
4. Most basic way to run your application on Ec2 Instance 
	- Get an EC2 Machine 
	- Install docker
	- docker run image (fetch from dockerhub)
	- That's it. (dumbest way)
![[Screenshot 2024-07-01 at 8.00.28 PM.png]]

Types of networks

- **Bridge**: The default network driver for containers. When you run a container without specifying a network, it's attached to a bridge network. It provides a private internal network on the host machine, and containers on the same bridge network can communicate with each other.

- **Host**: Removes network isolation between the container and the Docker host, and uses the host's networking directly. This is useful for services that need to handle lots of traffic or need to expose many ports. (we can figure this out someday later for sure)


### Docker composer 
Hehehe , we will go through you bad boy, don't worry, we will cover everything from now on