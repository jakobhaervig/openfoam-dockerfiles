FROM ubuntu:focal

ENV DEBIAN_FRONTEND=noninteractive

ENV TZ=Europe/Copenhagen
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# install essentials
RUN apt-get update && apt-get install -y \
		ssh \
		sudo \
		wget \
		nano \
		git \
		ffmpeg \
		build-essential \
		software-properties-common ;\
		rm -rf /var/lib/apt/lists/*

# install python
RUN apt-get update && apt-get install -y --no-install-recommends \
    python3 \
    python3-pip \
    && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
    
# install python packages
RUN pip3 install numpy
RUN pip3 install matplotlib

# download openfoam
RUN wget -O - https://dl.openfoam.org/gpg.key | apt-key add - && \
	add-apt-repository http://dl.openfoam.org/ubuntu && \
	apt-get update && \
	apt-get install -y openfoam9 paraviewopenfoam56- && \
	rm -rf /var/lib/apt/lists/*

# add user "foam"
RUN useradd --user-group --create-home --shell /bin/bash foam && \
	echo "foam ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# source openfoam and fix docker mpi
RUN	echo "source /opt/openfoam9/etc/bashrc" >> ~foam/.bashrc &&\
	echo "export OMPI_MCA_btl_vader_single_copy_mechanism=none" >> ~foam/.bashrc

# change environmental variables to make sure $WM_PROJECT_USER_DIR is outside of the container
RUN sed -i '/export WM_PROJECT_USER_DIR=/cexport WM_PROJECT_USER_DIR="/data/$WM_PROJECT/foam-$WM_PROJECT_VERSION"' /opt/openfoam9/etc/bashrc

# change user to "foam"
USER foam