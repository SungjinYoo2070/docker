# Start with Ubuntu base image
FROM ubuntu:16.04
MAINTAINER Mario Cho <hephaex@gmail.com>

# Install build-essential, git, python-dev, pip and other dependencies
RUN apt-get -y update && apt-get -y dist-upgrade && apt-get install -y \
  build-essential \
  git \
  pkg-config \
  cython \
  python-dev \
  python-pip \
  python-virtualenv \
  libhdf5-dev \
  libopencv-dev \
  libyaml-dev

#install h5py
RUN HDF5_DIR=/usr/lib/x86_64-linux-gnu/hdf5/serial/ pip install h5py
#install pip
RUN curl -O https://bootstrap.pypa.io/get-pip.py && \
    python get-pip.py && \
    rm get-pip.py
#install IPython
#RUN pip install ipython jupyter matplotlib
RUN pip --no-cache-dir install \
        ipykernel \
        jupyter \
        matplotlib \
        numpy \
        scipy \
        sklearn \
        pandas \
        Pillow \
        && \
    python -m ipykernel.kernelspec
# Clone neon repo and move into it
RUN cd /root && git clone https://github.com/NervanaSystems/neon.git && cd neon && \
# Make (no multithreading to prevent concurrency errors)
  make sysinstall
# Set ~/neon as working directory
WORKDIR /root/neon
CMD ipython notebook --ip 0.0.0.0 
