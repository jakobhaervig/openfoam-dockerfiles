FROM ubuntu:focal

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
	&& apt-get install -y nano curl sudo make g++

RUN useradd --user-group --create-home --shell /bin/bash foam ;\
	echo "foam ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

RUN curl -s https://dl.openfoam.com/add-debian-repo.sh | bash ;\
	apt-get install -y openfoam2006-default ;\
	rm -rf /var/lib/apt/lists/*

USER foam

RUN sudo sed -i 's+export WM_PROJECT_USER_DIR="$HOME/$WM_PROJECT/$USER-$WM_PROJECT_VERSION"+export WM_PROJECT_USER_DIR="/data/$WM_PROJECT/foam-$WM_PROJECT_VERSION"+g' /usr/lib/openfoam/openfoam2006/etc/bashrc

RUN	echo "source /usr/lib/openfoam/openfoam2006/etc/bashrc" >> ~foam/.bashrc ;\
	echo "export OMPI_MCA_btl_vader_single_copy_mechanism=none" >> ~foam/.bashrc
