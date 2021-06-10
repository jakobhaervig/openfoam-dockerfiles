FROM ubuntu:focal

ENV DEBIAN_FRONTEND=noninteractive

RUN rm /bin/sh && ln -s /bin/bash /bin/sh

#install essentials
RUN apt-get update \
	&& apt-get install -y \
		ssh \
		sudo \
		ffmpeg \
		wget \
		nano \
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
    
#install python packages
RUN pip3 install numpy

#download openfoam v8
RUN wget -O - http://dl.openfoam.org/gpg.key | apt-key add - ;\
	add-apt-repository http://dl.openfoam.org/ubuntu ;\
	apt-get update ;\
	apt-get install -y openfoam8 paraviewopenfoam56- ;\
	rm -rf /var/lib/apt/lists/*

#add user "foam"
RUN useradd --user-group --create-home --shell /bin/bash foam ;\
	echo "foam ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

#source openfoam and fix docker mpi
RUN	echo "source /opt/openfoam8/etc/bashrc" >> ~foam/.bashrc ;\
	echo "export OMPI_MCA_btl_vader_single_copy_mechanism=none" >> ~foam/.bashrc

#change user to "foam"
USER foam

#change environmental variables to make sure $WM_PROJECT_USER_DIR is outside of the container
RUN sudo sed -i 's+export WM_PROJECT_USER_DIR="$HOME/$WM_PROJECT/$USER-$WM_PROJECT_VERSION"+export WM_PROJECT_USER_DIR="/data/$WM_PROJECT/foam-$WM_PROJECT_VERSION"+g' /opt/openfoam8/etc/bashrc
