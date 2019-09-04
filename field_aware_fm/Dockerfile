# Build an image that can do training and inference in SageMaker
# This is a Python 3 image that uses the nginx, gunicorn, flask stack
# for serving inferences in a stable way.

FROM ubuntu:18.04

MAINTAINER Amazon AI <sage-learner@amazon.com>


RUN apt-get -y update && apt-get install -y --no-install-recommends \
         wget \
         python3-pip python3-dev \
         python-setuptools\
         nginx \
         ca-certificates \
         build-essential cmake \
         libopenblas-dev \
         make\
         gcc \
         g++\
         libboost-all-dev\
         protobuf-compiler\
         git \
         libx11-dev\
         libc6-dev\
         libgsl0-dev\
         libeigen3-dev


RUN cd /usr/local/bin \
  && ln -s /usr/bin/python3.6 python \
  && pip3 install --upgrade pip

# Here we get all python packages.
# There's substantial overlap between scipy and numpy that we eliminate by
# linking them together. Likewise, pip leaves the install caches populated which uses
# a significant amount of space. These optimizations save a fair amount of space in the
# image, which reduces start up time.
RUN wget https://bootstrap.pypa.io/get-pip.py && python get-pip.py && \
    pip3 install numpy scipy scikit-learn pandas flask gevent gunicorn cython xlearn 

ENV PATH="/opt/program:${PATH}"
# Set up the program in the image
COPY fm /opt/program
WORKDIR /opt/program
 


