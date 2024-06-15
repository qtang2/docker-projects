# docker-projects

# L05-02

Open a command prompt/terminal or use built-in terminal in Code using the **Terminal/New Terminal** menu or the **Ctrl-Shift-`** shortcut (that's a backtick).

Type the following Docker commands:

## Displays system information

    docker info

## Displays the system’s version

    docker version

## Log in to Docker Hub

    docker login


# L05-04

Type the following Docker commands:

## Pull and run a Nginx server

    docker run -d -p 8080:80 --name webserver nginx (--name name_of_running_instance name_of_the_image, When you use docker run -d, it starts the container in the background and returns the container ID. The container will continue to run until it is explicitly stopped or it exits on its own.)

## List the running containers

    docker ps

## List the images

    docker images

## Attach to the container

    docker container exec -it  webserver bash  

Exit by typing

    exit

## Stop the container

    docker stop webserver

## Remove the container from memory

    docker rm webserver

## Remove the image

    docker rmi nginx


# L08-03

## Open a terminal and create a volume

    docker volume create myvol

## List the volumes

    docker volume ls

## Run a Nginx container that will use the volume

    docker run -d --name voltest -v myvol:/app nginx:latest

## Connect to the instance

    docker exec -it voltest bash

## Let’s create a file in the volume using Nano

    apt-get update
    apt-get install nano

## Create a file in the app folder
    cd app
    nano test.txt

Type something, save the file and exit Nano using:

    CTRL-O
    CTRL-X

Detach from the instance:

    exit

## Stop and remove the container

    docker stop voltest
    docker rm voltest

## Run it again and see if the file still exists

    docker run -d --name voltest -v myvol:/app nginx:latest
    docker exec -it voltest bash
    cd app
    cat test.txt

## Cleanup

    docker volume rm myvol
    docker stop voltest
    docker rm voltest


# L09-04

## Build the app

    docker compose build

## Run the app

    docker compose up -d

When the app will run, launch the voting app in your browser http://localhost:5000


## List the containers

    docker compose ps

## Look at the db container logs

    docker compose logs -f web-fe


## Compose V2 commands

LS will list the current projects

    docker compose ls

## Let's try to deploy a second version

    docker compose up -d

This fails because we can only run an app a single time

## Deploy a second version using a different project name

Let's now use a project name to see if we can deploy a second version

    docker compose -p test up -d

This fails because the localhost port 5000 is already assigned.

Change the ports value from

    - "5000:80"

to

    - "5001:80"

## Deploy again

    docker compose -p test up -d

How many versions do we have running?

    docker compose ls

## Cleanup

    docker compose down
    docker compose ls
    docker compose -p test down
    docker compose ls


# L09-04

## Build the app

    docker compose build

## Run the app

    docker compose up -d

When the app will run, launch the voting app in your browser http://localhost:5000


## List the containers

    docker compose ps

## Look at the db container logs

    docker compose logs -f web-fe


## Compose V2 commands

LS will list the current projects

    docker compose ls

## Let's try to deploy a second version

    docker compose up -d

This fails because we can only run an app a single time

## Deploy a second version using a different project name

Let's now use a project name to see if we can deploy a second version

    docker compose -p test up -d

This fails because the localhost port 5000 is already assigned.

Change the ports value from

    - "5000:80"

to

    - "5001:80"

## Deploy again

    docker compose -p test up -d

How many versions do we have running?

    docker compose ls

## Cleanup

    docker compose down
    docker compose ls
    docker compose -p test down
    docker compose ls


# L10-03

## Docker Hub

Head to https://hub.docker.com and make sure you can log in.

## Add a Dockerfile file

Using the Code tooling, add a new Dockerfile by opening the Command Palette from the View menu.

Type **Docker Add** and select **Docker Add Docker Files to Workspace**.

## Tag using your Docker account name

For the next commands, replace `<YourRegistryName>` with your registry name.

## Build the image

    docker build -t <YourRegistryName>/express:v1 .

## Push the image

    docker push <YourRegistryName>/express:v1

## Docker Hub

Back in hub.docker.com, locate the image you just pushed.

## Pull the image from Docker Hub

Let’s first delete the local image and pull it back from Docker Hub.

## Remove the image

    docker rmi <YourRegistryName>/express:v1

## Pull the image

    docker pull <YourRegistryName>/express:v1

---

## Create version 2

Using the commands you learned earlier, build and push this new version to Docker Hub.

## Build the v2 image

    docker build -t <YourRegistryName>/express:v2 .

## push the image

    docker push <YourRegistryName>/express:v2

## Docker Hub

Back in hub.docker.com, locate the image you just pushed.

## Remove the local image

    docker rmi <YourRegistryName>/express:v2

## Pull the image

    docker pull <YourRegistryName>/express:v1

## Cleanup

    docker rmi <YourRegistryName>/express:v1
    docker rmi <YourRegistryName>/express:v2


# L18-02

## Current context

Get the current context:

    kubectl config current-context

## List all contexts

List all the contexts:

    kubectl config get-contexts

## Change context

Use a context:

    kubectl config use-context [contextName]

## Using kubectx

What's great about Kubernetes is the incredible amount of tools created by the community and available for free.  Kubectx is a simple tool that provides an easy way to list and change context.

You can install it on:

Windows (if you have Chocolatey installed):

    choco install kubectx-ps

macOS (if you have Brew installed):

    brew install kubectx

Ubuntu:

    sudo apt install kubectx

To list the contexts, simply type:

    kubectx

To change context:

    kubectx <contextName>

## Rename context

Rename context:

    kubectl config rename-context [old-name] [new-name]

## Delete context

Delete context:

    kubectl config delete-context [contextName]


# L18-04

Let's deploy an Nginx container using both methods.

## Imperative

    kubectl create deployment mynginx1 --image=nginx

## Declarative

    kubectl create -f deploy-example.yaml

## Cleanup

    kubectl delete deployment mynginx1
    kubectl delete deploy mynginx2