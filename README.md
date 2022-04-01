# OpenFOAM Dockerfiles

This repository contains OpenFOAM Dockerfiles. I've included both openfoam.com and openfoam.org releases based on Ubuntu Focal (20.04 LTS).

### What is Docker and why?

Docker is a set of tools to manage, build and run various software installations with a number of advantages. Using Docker we start containers (think of shipping containers)from images. Containers include everything needed to run a particular set of tasks (in this case OpenFOAM simulations). As containers are standardised, you can be confident that they run the same way on Windows, macOS and Linux. And yes, they are future proof and run similarly on major cloud solutions such as Amazon Web Services (AWS) and Microsoft Azure. This is convenient (!) because we can copy our setup to a cloud solution or a friend’s computer and still be confident it runs the same way.

### Docker containers, Docker images and Dockerfiles

Instead of shipping the complete container including the operating system, it’s more convenient to use what we call Dockerfiles. Think of Dockerfiles as recipes (simply just text file with set of commands) that outlines how to build an image. A container may then be started from the Docker image

# Setup

In the following, ```<version>``` refers to the OpenFOAM version (names of folders correspond to 
available versions), e.g. to install OpenFOAM v2112 you should ```<version>``` with v2112 throughout this guide.

## 1. Prerequisites
*1a)* Install [Docker](https://www.docker.com/products/docker-desktop)

Windows only: You will be prompted to install WSL (Windows Subsystem for Linux) when installing Docker (in the instructions
please follow step 4 and 5).

*1b)* Install [Git](https://git-scm.com/downloads)

*1c)* Install [Paraview](https://www.paraview.org/download/)

## 2. Initial setup
*2a)* Open a Powershell (Windows) or a terminal (macOS or Linux) and run the following commands to make a folder for your OpenFOAM data. This folder will store your simulation results and developments:

```shell
$ mkdir $HOME/openfoam-data
```

*2b)* Next, clone this repository by:

```shell
$ git clone https://github.com/jakobhaervig/openfoam-dockerfiles.git $HOME/openfoam-dockerfiles
```

You should now have two folder "openfoam-data" and "openfoam-dockerfiles" in your home folder.

*2c)* Now, make sure Docker is running before running before continuing.

*2d)* Build a OpenFOAM image. Remember to replace ```<version>```:

```shell
$ docker image build -t openfoam:<version> $HOME/openfoam-dockerfiles/<version>/
```

## 3. Running the Docker container

*3a)* Finally, we can run a Docker container with ``/data`` mapped to ``$HOME/openfoam-data``:

```shell
docker container run -ti --rm -v $HOME/openfoam-data:/data -w /data openfoam:<version>
```

*Please note* that everything in the container is deleted when you exit the container. Therefore you should save your simulation results and solver development in ``/data``, which is the only directory that persists when the container is closed.

Running the above command should leave you inside the Docker container with the username "foam". 
Also, you may access the container through ``$HOME/openfoam-data`` e.g.:

On a Windows system: ``C:\Users\jakob\openfoam-data``

On a macOS system: ``/Users/jakob/openfoam-data``

On most Linux systems: ``/home/jakob/openfoam-data``