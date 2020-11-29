# OpenFOAM Dockerfiles

This repository contains OpenFOAM Dockerfiles. I've included both openfoam.com and openfoam.org releases based on Ubuntu Focal (20.04 LTS).

## Instructions

Download a Dockerfile, navigate to the file in the terminal and build an image, e.g. "openfoam:v8" by: 

```shell
docker image build -t openfoam:v8 .

```

## Tips and tricks

When the image is build, you can launch your newly created image by:

```shell
docker container run -ti --rm -v $HOME:/data -w /data openfoam:v8
```
which will create an interactive session with access to the given openfoam installation. Furthermore, it will mount your $HOME folder as /data in your container. The contained is destroyed once you exit. You should therefore run your simulations inside /data, which is stored on your local file system.
