############################################################
# Dockerfile to build  container images
# Based on Ubuntu
############################################################
# Set the base image to Ubuntu
FROM ubuntu:12.04
# File Author / Maintainer
MAINTAINER Hartmut Schultze
# Update the repository sources list
RUN apt-get update
# Install compiler and perl stuff
RUN apt-get install --yes build-essential gcc-multilib apt-utils zlib1g-dev git
RUN apt-get clean
RUN apt-get remove --yes --purge build-essential gcc-multilib apt-utils zlib1g-dev vim git
WORKDIR /root