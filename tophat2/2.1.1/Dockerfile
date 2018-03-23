#################################################################
# Dockerfile to build TopHat 2.1.1 with Bowtie 2.3.4.1 container 
# images
# Based on Ubuntu
##################################################################

# Set the base image to Ubuntu
FROM ubuntu:14.04

# File/Author / Maintainer
MAINTAINER Kathrin Klee

# Update the repository sources list, install wget, unzip, python
RUN apt-get update && apt-get install --yes wget unzip python

# Working directory in /bin
WORKDIR /bin

# Download TopHat2
RUN wget https://ccb.jhu.edu/software/tophat/downloads/tophat-2.1.1.Linux_x86_64.tar.gz
# Download Bowtie2
RUN wget --default-page=bowtie2-2.3.4.1-linux-x86_64.zip https://sourceforge.net/projects/bowtie-bio/files/bowtie2/2.3.4.1/bowtie2-2.3.4.1-linux-x86_64.zip/
# Unzip the archive
RUN tar zxvf tophat-2.1.1.Linux_x86_64.tar.gz
# Remove the archive
RUN rm tophat-2.1.1.Linux_x86_64.tar.gz
# Unzip the archive
RUN unzip bowtie2-2.3.4.1-linux-x86_64.zip
# Remove the archive
RUN rm bowtie2-2.3.4.1-linux-x86_64.zip

# Working directory in Bowtie2
WORKDIR /bin/bowtie2-2.3.4.1
# Symbolic link from "bowtie" to "bowtie2"
RUN ln -s bowtie2 bowtie
# Change in PATH
ENV PATH $PATH:/bin/tophat-2.1.1.Linux_x86_64
ENV PATH $PATH:/bin/bowtie2-2.3.4.1

# Remove wget and unzip
RUN apt-get purge --yes wget unzip
# Working directory 
WORKDIR /
