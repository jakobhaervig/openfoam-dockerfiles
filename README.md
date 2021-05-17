# OpenFOAM Dockerfiles

This repository contains OpenFOAM Dockerfiles. I've included both openfoam.com and openfoam.org releases based on Ubuntu Focal (20.04 LTS).

## Setup

First, create a folder for your OpenFOAM files in your native OS, e.g.:

```shell
mkdir $HOME/openfoam-data

```

Next, clone this repository by:

```shell
git clone https://github.com/jakobhaervig/openfoam-dockerfiles.git $HOME/openfoam-dockerfiles

```
Now, make sure Docker is running before running before building the OpenFOAM image, e.g. for OpenFOAM v8:

```shell
docker image build -t openfoam:v8 $HOME/openfoam-dockerfiles/v8/

```

## Running the Docker container

Now, make sure Docker is running before running:

docker container run -ti --rm -v $HOME/openfoam-data:/data -w /data openfoam:v8

container. The contained is destroyed once you exit. You should therefore run your simulations inside /data, which is stored on your local file system.
