############################################################
# Dockerfile to build HISAT container images
# Based on Ubuntu
############################################################

# Set the base image to Ubuntu
FROM ubuntu:14.04

# File Author / Maintainer
MAINTAINER Hartmut Schultze 

# Update the repository sources list
RUN apt-get update  && apt-get -y install samtools=0.1.19-1 && apt-get install -y wget

# Install compiler and perl stuff
RUN apt-get install --yes build-essential git

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en  

# get NBCI Toolki
WORKDIR /tmp
RUN wget "http://ftp-trace.ncbi.nlm.nih.gov/sra/ngs/1.2.3/ngs-sdk.1.2.3-linux.tar.gz" && \
    tar zxfv ngs-sdk.1.2.3-linux.tar.gz

# Install HISAT
WORKDIR /tmp
RUN git clone https://github.com/infphilo/hisat.git
WORKDIR /tmp/hisat
RUN git checkout master

# Compile
RUN make USE_SRA=1 NCBI_NGS_DIR=/tmp/ngs-sdk.1.2.3-linux NCBI_VDB_DIR=/tmp/ngs-sdk.1.2.3-linux
RUN cp -p hisat hisat-* /usr/local/bin

# Cleanup
RUN rm -rf /tmp/hisat
RUN apt-get clean
RUN apt-get remove --yes --purge build-essential gcc-multilib apt-utils zlib1g-dev vim git

# Set default working path
WORKDIR /root

# Default command to execute at startup of the container
CMD hisat
