############################################################ 
# Dockerfile to build container images for C1 pipeline
# including STAR aligner and FastQC
# Based on Ubuntu 
############################################################ 

# Set the base image to Ubuntu 
FROM ubuntu:14.04 

# File Author / Maintainer 
MAINTAINER Kathrin Klee <klee@uni-bonn.de>

# Update the repository sources list 
RUN apt-get update && apt-get install -y openjdk-7-jre-headless && apt-get install -y unzip

# Install compiler and perl stuff 
RUN apt-get install --yes \
 build-essential \
 gcc-multilib \
 apt-utils \
 zlib1g-dev \
 vim-common \
 perl
 
# Install git 
RUN apt-get install -y git

# Install STAR 
WORKDIR /usr/local/
RUN pwd
RUN git clone https://github.com/alexdobin/STAR.git
WORKDIR /usr/local/STAR/
RUN pwd
RUN git checkout 2.5.1b 
WORKDIR /usr/local/STAR 
RUN pwd
RUN make STAR
ENV PATH /usr/local/STAR/source:$PATH

# Download FastQC
ADD http://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.5.zip /tmp/

# Install FastQC
RUN cd /usr/local && \
  unzip /tmp/fastqc_*.zip && \
  chmod 755 /usr/local/FastQC/fastqc && \
  ln -s /usr/local/FastQC/fastqc /usr/local/bin/fastqc && \
  rm -rf /tmp/fastqc_*.zip
