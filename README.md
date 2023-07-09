# Docker_Notes
This repo is for keeping all the docker knowledge in one place 

### Chapter 1 
# Introduction 

## What is docker 
Docker is a tool that helps you package and run applications in a consistent and isolated environment called a "container." Imagine a container as a lightweight, self-contained box that holds everything your application needs to run, such as the code, dependencies, libraries, and system tools.

Let's say you're building a web application using a specific programming language and some libraries. Without Docker, you'd have to worry about installing the correct version of the programming language, managing the dependencies, and configuring the environment on every machine where you want to run your application. This can be time-consuming and error-prone.

With Docker, you create a container that includes your application and all its dependencies. This container is based on a standardized image, which is like a blueprint for creating containers. You can think of an image as a snapshot of a fully set up and ready-to-run application.

Here's a simple example: Let's say you're developing a Python web application that uses the Flask framework. Instead of installing Python, Flask, and other dependencies on your local machine, you can create a Docker image that includes all those components. Then, you can run that image as a Docker container on any machine that has Docker installed.

This way, you don't have to worry about whether the host machine has the correct versions of Python and Flask. Docker ensures that your application runs consistently and reliably, regardless of the underlying environment. It eliminates the "it works on my machine" problem.

Docker also allows you to easily share your application with others. You can package your Docker image and share it with your team or publish it to a public registry, so that others can download and run your application in the same environment you tested it in.

In summary, Docker simplifies the process of building, deploying, and running applications by providing a standardized and isolated environment. It helps ensure that your application runs consistently across different machines, making it easier to develop, collaborate, and share software.

## what is an image and a container 

Lets first understand the OS structure 
![OS](https://github.com/walleeva2018/Docker_Notes/blob/91729d838184408fd2b19cbc08b45ed211fd6f78/Os.png)

- Here Any app you run on your computer creates a system call . That is basically saying hey computed i wan this much of memory and these commands to be executed
- Then the system call pass it to the kernel ( which is the controller of resource management in any Operating system)
- Kernel then assign resouces ( memory , CPU , Virtual memory etc to run some app )

Now lets understand what is an image 
![Image](https://github.com/walleeva2018/Docker_Notes/blob/91729d838184408fd2b19cbc08b45ed211fd6f78/image.png)

- There are 2 things here Controlller groups and Namespacing
- Namespacing is basically naming some resource and calling them by these name
- Controller groups are telling some resource that how much any app can use them
- So then an image is a combination of these namespacing and resources . And some extra commands that will execute these tasks

Now lets finally understand what is an container 
![Container](https://github.com/walleeva2018/Docker_Notes/blob/91729d838184408fd2b19cbc08b45ed211fd6f78/container.png)

- So then a  image call a startup command that will create an copy of all the instruction of the resources on Your computer
- The running these commands will create seperate resources and start using it
- No other app will be interupted by these Commands and no other app can access these resources
- SO you created a isolated computer inside your computer ( virtual machine) to run some tasks and that is ladies and gentleman called container
- 


### Chapter 2 
# Lets run some code 

Docker HUb: Docker Hub is a cloud-based repository provided by Docker where you can find and share Docker images. It serves as a centralized platform for storing and discovering pre-built Docker images created by the community.

To connect to Docker Hub from the terminal, you can follow these steps:

1. Install Docker: First, make sure Docker is installed on your machine. You can [download](https://docs.docker.com/get-docker/) and install Docker according to the instructions for your operating system.
   ``` docker --version``` to see whether it is installed properly 
2. Open an account in [docker hub](https://hub.docker.com/)  Remember the username and password
3. Open terminal and type ```docker login ```
4. A prompt will show up to give your username and password. After giving a message will indicate you are connected to docker hub 

Let print hello world 
Run this on your terminal 
``` docker run hello-world```

What this will do?

The docker run hello-world command is used to run a Docker container with the "hello-world" image. This command consists of two parts: the docker run command, which is used to start a container, and the image name hello-world, which refers to the specific Docker image you want to run.

When you execute this command, Docker checks if the "hello-world" image is available on your local machine. If it is not present locally, Docker automatically searches for the image on Docker Hub, which is a public registry for Docker images. Docker Hub is the default registry, but you can also use other registries if needed.

If the "hello-world" image is not found on your local machine, Docker pulls the image from Docker Hub to your local machine. The process of downloading the image is transparent to you, and Docker handles it automatically. Once the image is downloaded, Docker creates a container from that image and runs it.

The "hello-world" image is a simple image that contains a small, self-contained program. When you run the image, it prints a "Hello from Docker!" message to the console. This image is commonly used as a quick test to verify that Docker is correctly installed and running on your machine.

### Chapter 3
# All the commands

Now we will list all the necessary commands here . You can run them on your terminal and check whether its working like saide here

- ``` docker run <container-name> ls ```  Replace conatainer name with you preferable container from docker hub  
    It will list all the files that this image tells the machine to contain in itself aka all the files in the container
- ``` docker ps ```
    List all the running container in your machine
- ``` docker create <image-id> ``` remove image id with your preferable image id from docker hub
This creates all the necessary files but does not execute anything
- ``` docker start -a <container-id> ``` . You can get the container id from ```docker ps --all```
This one will start executing the container you created or the containers that are stopped
- ``` docker system prune ```
Removes all the containers from your machine . This is very important otherwise you machine will endup losing lots of stuff
- ``` docker logs <container-id> ```
Yes this just logs the output of the container
- ``` docker stop <container-id> ```
Yeah this one stops a container but gives it time to finish the current work or so
- ``` docker kill <container-id> ```
This one just kills it immediately
- ``` docker exec -it <container-id> <commands> ```
This command will execute any command on that container with input feature enabled
- ``` docker exec -it <container-id> sh ```
let you dicectly command your container without writing docker in front of them every time . sh is actually shell for that container

 
