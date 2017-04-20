############################################################
# Dockerfile to build container images for ATAC-seq pipeline
# including Bowtie1, samtools and Picard
# Based on Ubuntu
############################################################

# Set the base image to CentOS
FROM ubuntu:14.04

# File Author / Maintainer
MAINTAINER Kathrin Klee <klee@uni-bonn.de>

# Update the repository sources list and install samtools
RUN apt-get update

# Install some utilities
RUN apt-get install --yes build-essential \
    gcc-multilib \
    apt-utils \
    zlib1g-dev \
    curl \
    python \
    python2.7-dev \
    python-dev \
    cmake \
    libboost-all-dev \
    git \
    wget \
    unzip

# Install bcl2fastq
RUN cd /tmp/ && \
    wget https://support.illumina.com/content/dam/illumina-support/documents/downloads/software/bcl2fastq/bcl2fastq2-v2.19.0.tar.gz && \
    tar -xvzf bcl2fastq2-v2.19.0.tar.gz && \
    cd bcl2fastq && \
    ./src/configure --prefix=/tmp/bcl2fastq/ && \
    make && \
    make install

# Install cellranger
RUN cd /tmp/ && \
    mkdir cellranger && \
    cd cellranger && \
    wget --no-check-certificate -O cellranger-1.3.1.tar.gz "https://s3-us-west-2.amazonaws.com/10x.files/releases/cell-exp/cellranger-1.3.1.tar.gz?AWSAccessKeyId=AKIAJAZONYDS6QUPQVBA&Expires=1492737548&Signature=vhCwvuR6SV4LhMTn%2FTAptd\
0461w%3D"&& \
    cp cellranger-1.3.1.tar.gz /opt/ && \
    cd /opt/ && \
    tar zxf cellranger-1.3.1.tar.gz && \
    rm -f cellranger-1.3.1.tar.gz

# Shell script for CMD to setup ENV
RUN mkdir /opt/bin/ && \
    cd /tmp/ && \
    git clone https://github.com/genome/docker-cellranger.git && \
    cd docker-cellranger && \
    cp cellranger /opt/bin && \
    rm -rf /tmp/docker-cellranger
RUN chmod 777 /opt/bin/cellranger

# CELL RANGER VERSION
ENV CELLRANGER_VERSION 1.3.1
