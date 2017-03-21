# mbuckler/tf-inception-deps
#
# Dockerfile to hold dependencies for the Tensorflow implementation
# of Inception

FROM nvidia/cuda:8.0-cudnn5-devel
WORKDIR /root

# Get required packages
RUN apt-get update && \
  apt-get install vim \
                  python-pip \
                  python-dev \
                  python-opencv \
                  python-tk \
                  libjpeg-dev \
                  libfreetype6 \
                  libfreetype6-dev \
                  zlib1g-dev \
                  cmake \
                  wget \
                  cython \
                  git \
                  -y

# Install Bazel
RUN apt-get install software-properties-common \
                    python3-software-properties \
                    python-software-properties \
                    unzip \
                    -y
RUN \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y oracle-java8-installer && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /var/cache/oracle-jdk8-installer
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle
RUN wget "https://github.com/bazelbuild/bazel/releases/download/0.4.5/bazel-0.4.5-installer-linux-x86_64.sh"
RUN chmod +x bazel-0.4.5-installer-linux-x86_64.sh
RUN ./bazel-0.4.5-installer-linux-x86_64.sh
ENV PATH $PATH:$HOME/bin

# Get required python modules
RUN pip install --upgrade pip
RUN pip install image \
                scipy \
                matplotlib \
                PyYAML \
                numpy \
                easydict \
                tensorflow-gpu
# Update numpy
RUN pip install -U numpy

# Add CUDA to the path
ENV LD_LIBRARY_PATH $LD_LIBRARY_PATH:/usr/local/cuda/lib64
ENV CUDA_HOME /usr/local/cuda
ENV PYTHONPATH /root/coco/PythonAPI
RUN ldconfig

