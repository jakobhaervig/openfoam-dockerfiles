FROM ubuntu:focal

ENV DEBIAN_FRONTEND=noninteractive

RUN rm /bin/sh && ln -s /bin/bash /bin/sh

RUN apt-get update \
	&& apt-get install -y \
		ssh \
		sudo \
		nano \
		wget \
		software-properties-common ;\
		rm -rf /var/lib/apt/lists/*

RUN wget -O - http://dl.openfoam.org/gpg.key | apt-key add - ;\
	add-apt-repository http://dl.openfoam.org/ubuntu ;\
	apt-get update ;\
	apt-get install -y openfoam8 paraviewopenfoam56- ;\
	rm -rf /var/lib/apt/lists/*

RUN useradd --user-group --create-home --shell /bin/bash foam ;\
	echo "foam ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER foam

RUN sudo sed -i 's+export WM_PROJECT_USER_DIR=$HOME/$WM_PROJECT/$USER-$WM_PROJECT_VERSION+export WM_PROJECT_USER_DIR=/data/$WM_PROJECT/foam-$WM_PROJECT_VERSION+g' /opt/openfoam8/etc/bashrc

RUN	echo "source /opt/openfoam8/etc/bashrc" >> ~foam/.bashrc ;\
	echo "export OMPI_MCA_btl_vader_single_copy_mechanism=none" >> ~foam/.bashrc
