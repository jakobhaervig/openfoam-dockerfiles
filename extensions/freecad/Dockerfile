FROM openfoam

USER root

# install freecad
RUN apt update 
RUN DEBIAN_FRONTEND=noninteractive apt install -y freecad mc vim htop

# do some cleaning up
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# switch back to user foam
USER foam