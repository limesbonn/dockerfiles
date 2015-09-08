#################################################################
# Dockerfile to build TopHat 2.0.14 with Bowtie 2.2.3 container 
# images
# Based on Ubuntu
##################################################################
# Set the base image to Ubuntu
FROM ubuntu:14.04
# File/Author / Maintainer
MAINTAINER 
# Update the repository sources list, install wget, unzip, python
RUN apt-get update && apt-get install --yes wget unzip python
# Working directory in /bin
WORKDIR /bin
# Remove wget and unzip
RUN apt-get purge --yes wget unzip
# Working directory 
WORKDIR /
