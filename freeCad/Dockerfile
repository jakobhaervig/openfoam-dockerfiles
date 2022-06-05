FROM openfoam:2112

# install essentials
RUN sudo apt update 
RUN sudo DEBIAN_FRONTEND=noninteractive apt install -y freecad mc htop vim
RUN sudo rm -rf /var/lib/apt/lists/*
		
RUN pip3 install openturns==1.19.post1
RUN pip3 install platypus-opt==1.0.4