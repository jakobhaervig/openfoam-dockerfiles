FROM openfoam

USER root

# install python
RUN apt-get update && apt-get install -y --no-install-recommends \
    python3-full \
    python3-pip

# do some cleaning up
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# install python packages
RUN pip3 install numpy
RUN pip3 install install matplotlib
RUN pip3 install install openturns==1.23
RUN pip3 install install platypus-opt==1.2.0

# switch back to user foam
USER foam