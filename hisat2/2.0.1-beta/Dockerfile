############################################################
# Dockerfile to build hisat2 container images
# Based on Ubuntu
############################################################

# Set the base image to Ubuntu
FROM ubuntu:14.04

# File Author / Maintainer
MAINTAINER Hartmut Schultze

# Update the repository sources list
RUN apt-get update

# Install compiler and perl stuff
RUN apt-get install --yes build-essential git

#-------------------------------Add user----------------------------------------------------------------------------------#
# Create a pipeline user:pipeman and group:ngsgroup

RUN useradd -m -s /bin/bash pipeman && \
  cd /home/pipeman && \
  echo "#bash config file for user pipeman" >> /home/pipeman/.bashrc

RUN groupadd ngsgroup && \
  usermod -aG ngsgroup pipeman && \
  usermod -aG sudo pipeman

#-----------------------------NGS TOOLS DIRECTORY------------------------------------------------------------------------#  
#make pipeline install dirs
RUN mkdir /usr/local/pipeline && \
  chown pipeman:ngsgroup /usr/local/pipeline && \
  chmod 775 /usr/local/pipeline
  
#-------------------------------PERMISSIONS--------------------------
RUN chmod -R 777 /usr/local/pipeline 
RUN chown -R pipeman:ngsgroup /usr/local/pipeline

# samtools, htslib, bcftools
RUN cd /usr/local/pipeline && \
    git clone --branch=develop git://github.com/samtools/htslib.git && \
    git clone --branch=develop git://github.com/samtools/bcftools.git && \
    git clone --branch=develop git://github.com/samtools/samtools.git && \
    cd /usr/local/pipeline/htslib && \
    autoconf && \
    ./configure  && \
    make && \
    make install && \
    cd /usr/local/pipeline/bcftools && \
    make && \
    make install && \
    cd /usr/local/pipeline/samtools && \
    make install    
    make && \

# Install hisat2
WORKDIR /tmp
RUN git clone https://github.com/infphilo/hisat2.git
WORKDIR /tmp/hisat2
RUN git checkout master

# Compile
RUN make
RUN cp -p hisat2 hisat2-* /usr/local/bin

# Cleanup
RUN rm -rf /tmp/hisat2
RUN apt-get clean
RUN apt-get remove --yes --purge build-essential gcc-multilib apt-utils zlib1g-dev vim git

# Set default working path
WORKDIR /root

# Default command to execute at startup of the container
CMD hisat2
