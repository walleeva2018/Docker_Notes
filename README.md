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
