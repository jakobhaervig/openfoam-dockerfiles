#start from clean Ubuntu 20.04 image
FROM ubuntu:focal 

#we need terminal access when setting up this image
ENV DEBIAN_FRONTEND=noninteractive

#install essentials (add more as you like)
RUN apt-get update \
	&& apt-get install -y \
		ssh \
		sudo \
		wget \
		nano \
		ffmpeg \
		build-essential \
		software-properties-common ;\
		rm -rf /var/lib/apt/lists/*

#install python
RUN apt-get update && apt-get install -y --no-install-recommends \
    python3 \
    python3-pip \
    && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
    
#install python packages (add more as you like)
RUN pip3 install numpy

#add user "foam" to our system
RUN useradd --user-group --create-home --shell /bin/bash foam ;\
	echo "foam ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

#download openfoam v2012
RUN wget -q -O - https://dl.openfoam.com/add-debian-repo.sh | sudo bash ;\
    apt-get install -y openfoam2012-default ;\
    rm -rf /var/lib/apt/lists/*
    
#source openfoam and fix docker mpi
RUN echo "source /usr/lib/openfoam/openfoam2012/etc/bashrc" >> ~foam/.bashrc ;\
    echo "export OMPI_MCA_btl_vader_single_copy_mechanism=none" >> ~foam/.bashrc

#change user to "foam"
USER foam

#change environmental variables in etc/bashrc to make sure 
#$WM_PROJECT_USER_DIR is outside of the container
RUN sudo sed -i 's+ \
export WM_PROJECT_USER_DIR="$HOME/$WM_PROJECT/$USER-$WM_PROJECT_VERSION"+ \
export WM_PROJECT_USER_DIR="/data/$WM_PROJECT/foam-$WM_PROJECT_VERSION"+g' \
/usr/lib/openfoam/openfoam2012/etc/bashrc

