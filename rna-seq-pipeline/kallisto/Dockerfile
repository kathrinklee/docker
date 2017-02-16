############################################################ 
# Dockerfile to build container images for RNA-seq pipeline
# including Kallisto, sleuth and sratools
# Based on bioconductor 
############################################################ 

FROM insilicodb/bioconductor

# File Author / Maintainer 
MAINTAINER Kathrin Klee <klee@uni-bonn.de>

# install dependencies first
RUN apt-get update  && apt-get install -y \
		build-essential \
		cmake \
		python \
		python-pip \
		python-dev \
		hdf5-tools \
		libhdf5-dev \
		hdf5-helpers \
		libhdf5-serial-dev \
		git \
		apt-utils

# install kallisto from source
WORKDIR /docker
RUN git clone https://github.com/pachterlab/kallisto.git 
WORKDIR /docker/kallisto
RUN mkdir build
WORKDIR /docker/kallisto/build 
RUN cmake .. && \
	make && \
	make install

# install sleuth
RUN echo 'source("https://bioconductor.org/biocLite.R")' > /tmp/packages.R
RUN echo 'biocLite("devtools")' >> /tmp/packages.R
RUN echo 'biocLite("pachterlab/sleuth")' >> /tmp/packages.R
RUN Rscript /tmp/packages.R
