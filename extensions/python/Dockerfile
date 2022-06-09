FROM openfoam/esi:latest

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
RUN pip3 install openturns==1.19.post1
RUN pip3 install platypus-opt==1.0.4