FROM openfoam

USER root

# install freecad
RUN sudo apt update 
RUN sudo DEBIAN_FRONTEND=noninteractive apt install -y freecad

# do some cleaning up
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# switch back to user foam
USER foam