#### Base Image
FROM ubuntu:24.04 AS setup-cpp-ubuntu-gcc

# RUN apt update && apt upgrade -y
RUN apt-get update -qq && \
    # install git, busybox, python, ...
    apt-get install -y --no-install-recommends \
        git wget pipx python-is-python3 findutils sudo vim nano less tar tree \
        symlinks coreutils iputils-ping iproute2 inetutils-traceroute && \
    # # install setup-cpp
    # npm install -g setup-cpp@v1.7.1 && \
    # # install the compiler and tools
    # setup-cpp \
    #     --nala true \
    #     --compiler gcc \
    #     --cmake true \
    #     --ninja true \
    #     --gcovr true \
    #     --doxygen true \
    #     --graphviz true \
    #     --ccache true \
    #     --python true \
    #     --make true && \
    # # cleanup
    # nala autoremove -y && \
    # nala autopurge -y && \
    apt-get clean && \
    # nala clean --lists && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp/*

ENTRYPOINT ["/bin/bash"]

#### Building (example)
#FIXME: FROM aminya/setup-cpp-ubuntu-gcc:24.04 AS builder
FROM setup-cpp-ubuntu-gcc AS builder

WORKDIR /home/workdir

ENTRYPOINT ["/bin/bash"]
