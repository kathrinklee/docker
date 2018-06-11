# Set the base image to debian based miniconda3
FROM conda/miniconda3

# File Author / Maintainer
MAINTAINER Kathrin Klee

RUN apt-get clean && apt-get update && apt-get install -y locales

RUN echo "LC_ALL=en_US.UTF-8" >> /etc/environment
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen
RUN echo "LANG=en_US.UTF-8" > /etc/locale.conf
RUN locale-gen en_US.UTF-8

RUN conda update conda

RUN conda config --add channels r
RUN conda config --add channels defaults
RUN conda config --add channels conda-forge
RUN conda config --add channels bioconda

RUN conda install -y trimmomatic=0.36
RUN conda install -y bowtie2=2.3.4.1
RUN conda install -y picard=2.18.4
RUN conda install -y bedtools=2.27.1
RUN conda install -y homer=4.9.1
RUN conda install -y samtools=1.8
RUN conda install -y macs2=2.1.1.20160309
