FROM openfoam/esi:latest

# install python
RUN sudo apt update 
RUN sudo apt install -y --no-install-recommends python3-pip 

# install python packages
RUN sudo pip3 install numpy
RUN sudo pip3 install matplotlib

# install essentials
RUN sudo apt update 
RUN sudo DEBIAN_FRONTEND=noninteractive apt install -y freecad mc htop vim
RUN sudo rm -rf /var/lib/apt/lists/*
RUN sudo apt clean
		
RUN sudo pip3 install openturns==1.19.post1
RUN sudo pip3 install platypus-opt==1.0.4
