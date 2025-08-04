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

- So then a image call a startup command that will create an copy of all the instruction of the resources on Your computer
- The running these commands will create seperate resources and start using it
- No other app will be interupted by these Commands and no other app can access these resources
- SO you created a isolated computer inside your computer ( virtual machine) to run some tasks and that is ladies and gentleman called container
-

### Chapter 2

# Lets run some code

Docker HUb: Docker Hub is a cloud-based repository provided by Docker where you can find and share Docker images. It serves as a centralized platform for storing and discovering pre-built Docker images created by the community.

To connect to Docker Hub from the terminal, you can follow these steps:

1. Install Docker: First, make sure Docker is installed on your machine. You can [download](https://docs.docker.com/get-docker/) and install Docker according to the instructions for your operating system.
   ` docker --version` to see whether it is installed properly
2. Open an account in [docker hub](https://hub.docker.com/) Remember the username and password
3. Open terminal and type `docker login `
4. A prompt will show up to give your username and password. After giving a message will indicate you are connected to docker hub

Let print hello world
Run this on your terminal
` docker run hello-world`

What this will do?

The docker run hello-world command is used to run a Docker container with the "hello-world" image. This command consists of two parts: the docker run command, which is used to start a container, and the image name hello-world, which refers to the specific Docker image you want to run.

When you execute this command, Docker checks if the "hello-world" image is available on your local machine. If it is not present locally, Docker automatically searches for the image on Docker Hub, which is a public registry for Docker images. Docker Hub is the default registry, but you can also use other registries if needed.

If the "hello-world" image is not found on your local machine, Docker pulls the image from Docker Hub to your local machine. The process of downloading the image is transparent to you, and Docker handles it automatically. Once the image is downloaded, Docker creates a container from that image and runs it.

The "hello-world" image is a simple image that contains a small, self-contained program. When you run the image, it prints a "Hello from Docker!" message to the console. This image is commonly used as a quick test to verify that Docker is correctly installed and running on your machine.

### Chapter 3

# All the basic commands

Now we will list all the necessary commands here . You can run them on your terminal and check whether its working like saide here

- `docker run <container-name> ls` Replace conatainer name with you preferable container from docker hub  
   It will list all the files that this image tells the machine to contain in itself aka all the files in the container
- `docker ps`
  List all the running container in your machine
- `docker create <image-id>` remove image id with your preferable image id from docker hub
  This creates all the necessary files but does not execute anything
- `docker start -a <container-id>` . You can get the container id from `docker ps --all`
  This one will start executing the container you created or the containers that are stopped
- `docker system prune`
  Removes all the containers from your machine . This is very important otherwise you machine will endup losing lots of stuff
- `docker logs <container-id>`
  Yes this just logs the output of the container
- `docker stop <container-id>`
  Yeah this one stops a container but gives it time to finish the current work or so
- `docker kill <container-id>`
  This one just kills it immediately
- `docker exec -it <container-id> <commands>`
  This command will execute any command on that container with input feature enabled
- `docker exec -it <container-id> sh`
  let you dicectly command your container without writing docker in front of them every time . sh is actually shell for that container

### Chapter 4

# Create Your own docker image

# Docker Tutorial - From Zero to Hero

## Step 1: Minimal Dockerfile (3 lines)

The absolute simplest Dockerfile to run our hello world:

```dockerfile
FROM node:18
COPY app.js .
CMD ["node", "app.js"]
```

**Build and Run:**
```bash
docker build -t hello-world-v1 .
docker run hello-world-v1
```

**Expected Output:**
```
Hello World from Docker!
```

**What you'll see during build:**
- Downloads node:18 image (first time only)
- Copies your app.js file
- Creates the image

**Try this too:**
```bash
# See what's inside the container
docker run -it hello-world-v1 /bin/bash
# Inside container: ls (you'll see app.js in root directory)
# Type: exit
```

---

## Step 2: Add Working Directory (4 lines)

Let's organize files properly:

```dockerfile
FROM node:18
WORKDIR /app
COPY app.js .
CMD ["node", "app.js"]
```

**Build and Run:**
```bash
docker build -t hello-world-v2 .
docker run hello-world-v2
```

**Expected Output:**
```
Hello World from Docker!
```

**What changed:** Files now go into `/app` directory inside container

**See the difference:**
```bash
# Compare with previous version
docker run -it hello-world-v1 /bin/bash
# Inside: ls (app.js is in root /)
# exit

docker run -it hello-world-v2 /bin/bash  
# Inside: pwd (you're in /app)
# Inside: ls (app.js is in /app)
# exit
```

**Key Learning:** WORKDIR makes your container organized!

---

## Step 3: Better Copy Strategy (5 lines)

Copy everything in current directory:

```dockerfile
FROM node:18
WORKDIR /app
COPY . .
EXPOSE 3000
CMD ["node", "app.js"]
```

**Build and Run:**
```bash
docker build -t hello-world-v3 .
docker run hello-world-v3
```

**Expected Output:**
```
Hello World from Docker!
```

**What changed:** 
- `COPY . .` copies all files (including this Dockerfile!)
- `EXPOSE 3000` documents which port we'll use (for web apps)

**See what got copied:**
```bash
docker run -it hello-world-v3 /bin/bash
# Inside: ls -la (you'll see Dockerfile, app.js, and any other files)
# exit
```

**Test the EXPOSE (doesn't actually publish ports yet):**
```bash
# This still works the same way
docker run hello-world-v3
```

**Key Learning:** COPY . . is convenient but copies everything! EXPOSE is just documentation.

---

## Step 4: Add Package Management (7 lines)

For real Node.js apps with dependencies:

```dockerfile
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "app.js"]
```

**First, create a package.json:**
```bash
echo '{"name":"hello-docker","version":"1.0.0","main":"app.js"}' > package.json
```

**Build and Run:**
```bash
docker build -t hello-world-v4 .
docker run hello-world-v4
```

**Expected Output:**
```
Hello World from Docker!
```

**What changed:** 
- Copy package.json first, then install dependencies
- This creates better Docker layer caching

**See the build difference:**
```bash
# Build again (should be faster due to caching)
docker build -t hello-world-v4 .
# Notice: "CACHED" appears for npm install step
```

**Explore the container:**
```bash
docker run -it hello-world-v4 /bin/bash
# Inside: ls -la (see node_modules folder)
# Inside: node --version
# exit
```

**Key Learning:** Layer caching saves time! Install dependencies before copying code.

---

## Step 5: Add Environment Variables (9 lines)

Make your app configurable:

```dockerfile
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
ENV NODE_ENV=production
ENV PORT=3000
EXPOSE 3000
CMD ["node", "app.js"]
```

**Build and Run:**
```bash
docker build -t hello-world-v5 .
docker run hello-world-v5
```

**Expected Output:**
```
Hello World from Docker!
```

**What changed:** Set environment variables with `ENV`

**Test environment variables:**
```bash
# Check the environment variables
docker run -it hello-world-v5 /bin/bash
# Inside: echo $NODE_ENV (should show: production)
# Inside: echo $PORT (should show: 3000)
# Inside: env | grep NODE (see all Node-related env vars)
# exit

# Override environment variables at runtime
docker run -e NODE_ENV=development hello-world-v5
# (Still same output, but env var is different inside)

# Verify the override:
docker run -it -e NODE_ENV=development hello-world-v5 /bin/bash
# Inside: echo $NODE_ENV (should show: development)
# exit
```

**Key Learning:** ENV sets defaults, but you can override them with -e flag!

---

## Step 6: Use Alpine for Smaller Images (9 lines)

Same functionality, much smaller size:

```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
ENV NODE_ENV=production
ENV PORT=3000
EXPOSE 3000
CMD ["node", "app.js"]
```

**Build and Run:**
```bash
docker build -t hello-world-v6 .
docker run hello-world-v6
```

**Expected Output:**
```
Hello World from Docker!
```

**What changed:** `node:18-alpine` is much smaller than regular `node:18`

**Compare image sizes:**
```bash
# Check the size difference
docker images | grep hello-world
# v5 (regular node): ~900MB
# v6 (alpine): ~170MB - Much smaller!
```

**Explore Alpine differences:**
```bash
docker run -it hello-world-v6 /bin/sh  # Note: /bin/sh not /bin/bash
# Inside: cat /etc/os-release (see Alpine Linux)
# Inside: ls /bin/ (fewer tools available)
# Inside: which bash (not found - Alpine uses sh)
# exit

# Compare with regular Ubuntu-based image:
docker run -it hello-world-v5 /bin/bash
# Inside: cat /etc/os-release (see Ubuntu/Debian)
# exit
```

**Key Learning:** Alpine = smaller size, fewer tools. Use -sh instead of -bash!

---

## Step 7: Add Security - Non-root User (12 lines)

Don't run as root for security:

```dockerfile
FROM node:18-alpine
RUN addgroup -g 1001 -S nodejs
RUN adduser -S nodejs -u 1001
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
USER nodejs
ENV NODE_ENV=production
ENV PORT=3000
EXPOSE 3000
CMD ["node", "app.js"]
```

**Build and Run:**
```bash
docker build -t hello-world-v7 .
docker run hello-world-v7
```

**Expected Output:**
```
Hello World from Docker!
```

**What changed:** Created user `nodejs` and switched to it with `USER`

**See the security difference:**
```bash
# Check who's running the process in v6 (root)
docker run -it hello-world-v6 /bin/sh
# Inside: whoami (shows: root)
# Inside: id (shows uid=0 - root user)
# exit

# Check who's running the process in v7 (nodejs user)
docker run -it hello-world-v7 /bin/sh
# Inside: whoami (shows: nodejs)
# Inside: id (shows uid=1001 - non-root user)
# Inside: ls -la (see file ownership)
# exit
```

**Test permission restrictions:**
```bash
docker run -it hello-world-v7 /bin/sh
# Inside: touch /etc/test-file (should fail - Permission denied)
# Inside: touch test-file (should work - can write in /app)
# exit
```

**Key Learning:** Non-root users can't modify system files - much safer!

---

## Step 8: Optimize Layer Caching (13 lines)

Better performance when rebuilding:

```dockerfile
FROM node:18-alpine
RUN addgroup -g 1001 -S nodejs
RUN adduser -S nodejs -u 1001
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY --chown=nodejs:nodejs . .
USER nodejs
ENV NODE_ENV=production
ENV PORT=3000
EXPOSE 3000
HEALTHCHECK CMD curl -f http://localhost:3000 || exit 1
CMD ["node", "app.js"]
```

**Build and Run:**
```bash
docker build -t hello-world-v8 .
docker run hello-world-v8
```

**Expected Output:**
```
Hello World from Docker!
```

**What changed:** 
- `npm ci` instead of `npm install` (faster, reliable)
- `--chown=nodejs:nodejs` sets file ownership
- Added `HEALTHCHECK`

**Test npm ci vs npm install:**
```bash
# Time the difference (npm ci is faster for production)
time docker build -t hello-world-v8-test .
```

**Check file ownership:**
```bash
docker run -it hello-world-v8 /bin/sh
# Inside: ls -la (all files owned by nodejs:nodejs)
# exit

# Compare with v7:
docker run -it hello-world-v7 /bin/sh  
# Inside: ls -la (files owned by root, but running as nodejs)
# exit
```

**Test health check:**
```bash
# For this simple app, healthcheck will fail (no web server)
# But you can see it in container inspect:
docker run -d --name health-test hello-world-v8
sleep 35  # Wait for health check
docker inspect health-test | grep -A 10 "Health"
docker rm -f health-test
```

**Key Learning:** --chown fixes permissions, npm ci is better for production!

---

## Step 9: Multi-stage Build (Advanced)

Separate build and runtime environments:

```dockerfile
# Build stage
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production

# Production stage  
FROM node:18-alpine AS production
RUN addgroup -g 1001 -S nodejs
RUN adduser -S nodejs -u 1001
WORKDIR /app
COPY --from=builder --chown=nodejs:nodejs /app/node_modules ./node_modules
COPY --chown=nodejs:nodejs . .
USER nodejs
ENV NODE_ENV=production
EXPOSE 3000
HEALTHCHECK CMD curl -f http://localhost:3000 || exit 1
CMD ["node", "app.js"]
```

**What changed:** Two stages - one for building, one for running

---

## Step 10: Production Ready with All Best Practices

```dockerfile
# Build stage
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production && npm cache clean --force

# Production stage
FROM node:18-alpine AS production

# Install security updates and dumb-init
RUN apk add --no-cache dumb-init curl

# Create user
RUN addgroup -g 1001 -S nodejs && \
    adduser -S nodejs -u 1001

# Set working directory
WORKDIR /app

# Copy from builder stage
COPY --from=builder --chown=nodejs:nodejs /app/node_modules ./node_modules
COPY --chown=nodejs:nodejs . .

# Switch to non-root user
USER nodejs

# Environment variables
ENV NODE_ENV=production
ENV PORT=3000

# Expose port
EXPOSE 3000

# Health check
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
    CMD curl -f http://localhost:3000/health || exit 1

# Use dumb-init for proper signal handling
ENTRYPOINT ["dumb-init", "--"]
CMD ["node", "app.js"]
```

**What changed:** Added signal handling, security updates, optimized RUN commands

---

## Quick Commands Summary:

```bash
# Build and run each version:
docker build -t hello-world-v[1-10] .
docker run hello-world-v[1-10]

# Interactive exploration:
docker run -it hello-world-v[1-10] /bin/bash  # or /bin/sh for Alpine
docker run -it hello-world-v[1-10] /bin/sh    # for Alpine versions

# Compare image sizes:
docker images | grep hello-world

# Clean up when done:
docker rmi hello-world-v1 hello-world-v2 hello-world-v3 # etc...
```

## 🎯 Key Learning Points:

1. **Start simple** - 3 lines can run any Node.js app
2. **WORKDIR organizes** - keeps files in proper directories  
3. **Layer caching** - Order matters! Put changing stuff last
4. **Environment variables** - ENV sets defaults, -e overrides
5. **Alpine = smaller** - but use /bin/sh instead of /bin/bash
6. **Security matters** - never run as root in production
7. **File ownership** - use --chown to fix permissions
8. **npm ci > npm install** - for production builds

## 🚀 Try This Progression:
1. Start with Step 1 - see it work
2. Compare each step with the previous one using -it
3. Notice the differences in size, security, and functionality
4. By Step 8, you understand all major Docker concepts!

**Pro Tip:** After each step, run `docker run -it [image-name] /bin/sh` to explore what's inside!


