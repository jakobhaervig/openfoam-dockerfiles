# OpenFOAM Dockerfiles

This repository contains OpenFOAM Dockerfiles. I've included both openfoam.com and openfoam.org releases based on Ubuntu Focal (20.04 LTS).

### What is Docker and why?

Docker is a set of tools to manage, build and run various software installations with a number of advantages. Using Docker we start containers (think of shipping containers)from images. Containers include everything needed to run a particular set of tasks (in this case OpenFOAM simulations). As containers are standardised, you can be confident that they run the same way on Windows, macOS and Linux. And yes, they are future proof and run similarly on major cloud solutions such as Amazon Web Services (AWS) and Microsoft Azure. This is convenient (!) because we can copy our setup to a cloud solution or a friend’s computer and still be confident it runs the same way.

### Docker containers, Docker images and Dockerfiles

Instead of shipping the complete container including the operating system, it’s more convenient to use what we call Dockerfiles. Think of Dockerfiles as recipes (simply just text file with set of commands) that outlines how to build an image. A container may then be started from the Docker image

# Setup

## 1. Prerequisites
a) Install [Docker](https://www.docker.com/products/docker-desktop)
Windows only: You will be prompted to install WSL (Windows Subsystem for Linux) when installing Docker (in the instructions
please follow step 4 and 5).

b) Install [Git](https://git-scm.com/downloads)

c) Install [Paraview](https://www.paraview.org/download/)

## 2. Initial setup
a) Open a Powershell (Windows) or a terminal (macOS or Linux) and run the following commands to make a folder for your OpenFOAM data. This folder will store your simulation resuslts:

```shell
mkdir $HOME/openfoam-data

```

b) Next, clone this repository by:

```shell
git clone https://github.com/jakobhaervig/openfoam-dockerfiles.git $HOME/openfoam-dockerfiles

```
c) Now, make sure Docker is running before running before continuing.

d) Build the OpenFOAM image, e.g. for OpenFOAM v2106:

```shell
docker image build -t openfoam:v2106 $HOME/openfoam-dockerfiles/v2106/

```



## Running the Docker container

Now, make sure Docker is running before running:

```shell
docker container run -ti --rm -v $HOME/openfoam-data:/data -w /data openfoam:v2106

```

You may want to create an alias for the above command:

```shell
echo 'alias of2106="docker container run -ti --rm -v $HOME/openfoam-data:/data -w /data openfoam:v2106"' >> $HOME/.bashrc
```

Now you start a new Docker container with the alias of2106.
