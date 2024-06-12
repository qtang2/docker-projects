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