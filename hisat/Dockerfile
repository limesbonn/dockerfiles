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

# clone repo sra-toolkit
WORKDIR /src
RUN wget "http://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/2.5.7/sratoolkit.2.5.7-ubuntu64.tar.gz" && \
    tar zxfv sratoolkit.2.5.7-ubuntu64.tar.gz && \
    cp -r sratoolkit.2.5.7-ubuntu64/bin/* /usr/bin

# Install HISAT
WORKDIR /tmp
RUN git clone https://github.com/infphilo/hisat.git
WORKDIR /tmp/hisat
RUN git checkout master

# Compile
RUN make
RUN cp -p hisat hisat-* /usr/local/bin

# Cleanup
RUN rm -rf /tmp/hisat
RUN apt-get clean
RUN apt-get remove --yes --purge build-essential gcc-multilib apt-utils zlib1g-dev vim git

# Set default working path
WORKDIR /root

# Default command to execute at startup of the container
CMD hisat
