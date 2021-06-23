FROM ubuntu:focal

ENV DEBIAN_FRONTEND=noninteractive

#install essentials
RUN apt-get update \
	&& apt-get install -y \
		ssh \
		sudo \
		wget \
		nano \
		build-essential \
		software-properties-common ;\
		rm -rf /var/lib/apt/lists/*

#install python
RUN apt-get update && apt-get install -y --no-install-recommends \
    python3 \
	net-tools \
	libgl1-mesa-glx \
	libpng16-16 \
	gfortran-7 \
    python3-pip \
    && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
    
#install python packages
RUN pip3 install numpy
RUN pip3 install platypus-opt
RUN pip3 install matplotlib

#add user "foam"
RUN useradd --user-group --create-home --shell /bin/bash foam ;\
	echo "foam ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

#download openfoam v2012
RUN wget -q -O - https://dl.openfoam.com/add-debian-repo.sh | sudo bash ;\
    apt-get install -y openfoam2012-default ;\
    rm -rf /var/lib/apt/lists/*

#download salome v9.4.0
RUN mkdir /opt/salome
RUN wget -O SALOME-9.4.0-UB18.04-SRC.tar.gz "https://www.salome-platform.org/downloads/previous-versions/salome-v9.4/DownloadDistr?platform=SP.UB18.04&version=9.4.0"
RUN tar zxfv SALOME-9.4.0-UB18.04-SRC.tar.gz -C /opt/salome --strip-components 1
RUN rm SALOME-9.4.0-UB18.04-SRC.tar.gz

#source openfoam and fix docker mpi
RUN echo "source /usr/lib/openfoam/openfoam2012/etc/bashrc" >> ~foam/.bashrc ;\
    echo "export OMPI_MCA_btl_vader_single_copy_mechanism=none" >> ~foam/.bashrc

#change user to "foam"
USER foam

RUN echo 'alias salome="/opt/salome/salome"' >> ~foam/.bashrc

#change environmental variables to make sure $WM_PROJECT_USER_DIR is outside of the container
RUN sudo sed -i 's+export WM_PROJECT_USER_DIR="$HOME/$WM_PROJECT/$USER-$WM_PROJECT_VERSION"+export WM_PROJECT_USER_DIR="/data/$WM_PROJECT/foam-$WM_PROJECT_VERSION"+g' /usr/lib/openfoam/openfoam2012/etc/bashrc