############################################################ 
# Dockerfile to build container images for discovardenovo
# Based on biodocker
############################################################ 

# Set the base image to Ubuntu
FROM biodckr/biodocker

# File Author / Maintainer
MAINTAINER Kathrin Klee <klee@uni-bonn.de>

# Change user to root
USER root

# Install jemalloc
ENV ZIP=jemalloc-4.5.0.tar.bz2
ENV URL=https://github.com/jemalloc/jemalloc/releases/download/4.5.0
ENV FOLDER=jemalloc-4.0.2
ENV DST=/tmp

RUN wget $URL/$ZIP -O $DST/$ZIP && \
    tar xvf $DST/$ZIP -C $DST && \
    rm $DST/$ZIP && \
    cd $DST/$FOLDER && \
    ./configure && \
    make && \
    make install && \
    cd / && \
    rm -rf $DST/$FOLDER

# Install discovardenovo
ENV ZIP=discovardenovo-52488.tar.gz
ENV URL=ftp://ftp.broadinstitute.org/pub/crd/DiscovarDeNovo/latest_source_code
ENV FOLDER=discovardenovo-52488
ENV DST=/tmp

ENV MALLOC_PER_THREAD 1

RUN wget $URL/$ZIP -O $DST/$ZIP && \
    tar xvf $DST/$ZIP -C $DST && \
    rm $DST/$ZIP && \
    cd $DST/$FOLDER && \
    ./configure && \
    make && \
    make install && \
    cd / && \
    rm -rf $DST/$FOLDER

# Change user to back to biodocker
USER biodocker

# CHANGE WORKDIR TO /DATA
WORKDIR /data

# DEFINE DEFAULT COMMAND
# CMD ["discovardenovo"]

