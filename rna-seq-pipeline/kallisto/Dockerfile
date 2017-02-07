############################################################ 
# Dockerfile to build container images for RNA-seq pipeline
# including Kallisto and sratools
# Based on Ubuntu 
############################################################ 

# Set the base image from bioconductor 
FROM insilicodb/bioconductor

# File Author / Maintainer 
MAINTAINER Kathrin Klee <klee@uni-bonn.de>

# Update the repository sources list
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
  apt-utils \
  pigz
  
# install sra-toolkit
RUN wget "http://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/2.4.4/sratoolkit.2.4.4-ubuntu64.tar.gz" && \
    tar zxfv sratoolkit.2.4.4-ubuntu64.tar.gz && \
    cp -r sratoolkit.2.4.4-ubuntu64/bin/* /usr/bin
    
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
