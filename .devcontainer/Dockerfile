#### Base Image
FROM ubuntu:24.04 as setup-cpp-ubuntu-gcc

# ARG CMAKE_VERSION='3.28.1'
# ARG NINJA_VERSION='1.11.1'

# RUN apt update && apt upgrade -y
RUN apt-get update -qq && \
    # install git, nodejs, and npm
    apt-get install -y --no-install-recommends python-is-python3 \
        git pipx busybox less vim tree symlinks nodejs npm && \
    # install setup-cpp
    npm install -g setup-cpp@v1.7.1 && \
    # install the compiler and tools
    setup-cpp \
        --nala true \
        --compiler gcc \
        --cmake true \
        --ninja true \
        --gcovr true \
        --doxygen true \
        --graphviz true \
        --ccache true \
        --python true \
        --make true && \
    # cleanup
    nala autoremove -y && \
    nala autopurge -y && \
    apt-get clean && \
    nala clean --lists && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp/*

# COPY .devcontainer/scripts /tmp/scripts
# WORKDIR /tmp/scripts

# RUN bash g++.sh
# RUN bash llvm.sh
# RUN bash cmake.sh $CMAKE_VERSION
# RUN bash ninja.sh $NINJA_VERSION

# RUN bash googletest.sh '/opt'

# RUN rm -rf /tmp/scripts

ENTRYPOINT ["/bin/bash"]

#### Building (example)
#FIXME:
FROM aminya/setup-cpp-ubuntu-gcc:24.04 AS builder
#XXX FROM setup-cpp-ubuntu-gcc AS builder

WORKDIR /home/workdir

# COPY . /home/app
# WORKDIR /home/app
# RUN bash -c 'source ~/.cpprc \
#     && make all'

ENTRYPOINT ["/bin/bash"]
