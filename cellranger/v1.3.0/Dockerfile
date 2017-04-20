###################################################
# Dockerfile for Cell Ranger
###################################################

# Based on
FROM centos:7

# File Author / Maintainer
MAINTAINER Kathrin Klee <klee@uni-bonn.de>

# Install some utilities
RUN yum install -y \
	file \
	git \
	sssd-client \
	which \
	unzip

# Install bcl2fastq
RUN cd /tmp/ && \
	git clone git://git/bcl2fastq.git --branch v2.17.1 --single-branch bcl2fastq && \
	cd bcl2fastq/ && \
	yum -y --nogpgcheck localinstall bcl2fastq2-v2.17.1.14-Linux-x86_64.rpm && \
	cd /tmp/ && \
	rm -rf bcl2fastq/
	
# Install cellranger
RUN cd /tmp/ && \
	git clone git://git/10x-genomics-cellranger --branch v1.3.0 --single-branch cellranger && \
	cd cellranger && \
	cp cellranger-1.3.0.tar.gz /opt/ && \
	cd /opt/ && \
	tar zxf cellranger-1.3.0.tar.gz && \
	rm -f cellranger-1.3.0.tar.gz /cellranger

# Shell script for CMD to setup ENV
RUN mkdir /opt/bin/ && \
	cd /tmp/ && \
	git clone https://github.com/genome/docker-cellranger.git && \
	cd docker-cellranger && \
	cp cellranger /opt/bin && \
	rm -rf /tmp/docker-cellranger
RUN chmod 777 /opt/bin/cellranger

# CELL RANGER VERSION
ENV CELLRANGER_VERSION 1.3.0

# Entrypoint is the cellranger wrapper scipt
ENTRYPOINT ["/opt/bin/cellranger"]
