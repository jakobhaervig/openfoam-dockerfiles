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
Now, make sure Docker is running before running before building the OpenFOAM image, e.g. for OpenFOAM v2106:

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

## More detailed information

More information for Windows operating system is available at https://haervig.com/files/openfoam_with_docker.pdf
