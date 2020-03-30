FROM nvidia/cuda:8.0-cudnn6-devel-ubuntu16.04
LABEL maintainer caffe-maint@googlegroups.com

RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        cmake \
        git \
        wget \
        libatlas-base-dev \
        libboost-all-dev \
        libgflags-dev \
        libgoogle-glog-dev \
        libhdf5-serial-dev \
        libleveldb-dev \
        liblmdb-dev \
        libopencv-dev \
        libprotobuf-dev \
        libsnappy-dev \
        protobuf-compiler \
        python-dev \
        python-numpy \
        python-pip \
        python-setuptools \
        python-scipy && \
    rm -rf /var/lib/apt/lists/*

ENV CAFFE_ROOT=/opt/caffe
WORKDIR $CAFFE_ROOT

# FIXME: use ARG instead of ENV once DockerHub supports this
# https://github.com/docker/hub-feedback/issues/460
ENV CLONE_TAG=1.0

RUN git clone -b ${CLONE_TAG} --depth 1 https://github.com/BVLC/caffe.git . && \
    pip install --upgrade pip && \
    cd python && for req in $(cat requirements.txt) pydot; do pip install $req; done && cd .. && \
    mkdir build && cd build && \
    cmake -DUSE_CUDNN=1 .. && \
    make -j 2

ENV PYCAFFE_ROOT $CAFFE_ROOT/python
ENV PYTHONPATH $PYCAFFE_ROOT:$PYTHONPATH
ENV PATH $CAFFE_ROOT/build/tools:$PYCAFFE_ROOT:$PATH
RUN echo "$CAFFE_ROOT/build/lib" >> /etc/ld.so.conf.d/caffe.conf && ldconfig

WORKDIR /workspace
RUN pip install cycler==0.10.0
RUN pip install Cython==0.24.1
RUN pip install dask==0.10.2
RUN pip install decorator==4.0.10
RUN pip install matplotlib==1.5.1
RUN pip install networkx==1.11
RUN pip install numpy==1.11.1
RUN pip install Pillow==3.3.0
RUN pip install protobuf==3.0.0
RUN pip install pyparsing==2.1.5
RUN pip install pypng==0.0.18
RUN pip install python-dateutil==2.5.3
RUN pip install pytz==2016.6.1
RUN pip install scikit-image==0.12.3
RUN pip install --ignore-installed scipy==0.18.0
RUN pip install six==1.10.0
RUN pip install Theano==0.8.2
RUN pip install toolz==0.8.0

WORKDIR /workspace
RUN pip install opencv-python
RUN apt-get update && apt-get install locate
RUN pip install -U numpy
RUN pip install pydot-ng
RUN apt-get update && apt-get install -y vim
Run pip insyall scikit-learn
