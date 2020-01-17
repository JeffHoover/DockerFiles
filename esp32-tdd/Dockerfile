# This dockerfile uses Environment for ESP32 CI builds
#
# Ubuntu 18.04
# https://hub.docker.com/_/ubuntu
#
# Toolchain linux64-1.22.0-80-g6c4433a-5.2.0
# https://docs.espressif.com/projects/esp-idf/en/v3.2/get-started/linux-setup.html
#
# ESP-IDF v3.2
# https://docs.espressif.com/projects/esp-idf/en/v3.2/get-started/index.html#get-esp-idf
# adapted from https://hub.docker.com/r/larryli/esp-idf-ci-env/dockerfile
#
# TODO: 
# - python3 (currently Python 2.7.17) Note ubuntu comes with python 2.  It's not clear how to make python3 only.
# - latest toolchain?

FROM ubuntu:18.04
MAINTAINER Todd Flanders todd.a.flanders@accenture.com

ENV IDF_PATH="/opt/local/espressif/esp-idf" 
ENV PATH="/opt/local/espressif/xtensa-esp32-elf/bin:/root/cmake/bin:${IDF_PATH}/tools:${PATH}"
RUN apt-get update \
    && apt-get install -y gcc git wget make libncurses-dev flex bison gperf python python-pip python-setuptools python-serial python-cryptography python-future \
	&& rm -r /var/lib/apt/lists/*
RUN mkdir -p /opt/local/espressif/ \
    && wget -qO- https://dl.espressif.com/dl/xtensa-esp32-elf-linux64-1.22.0-80-g6c4433a-5.2.0.tar.gz \
    | tar xz -C /opt/local/espressif/
RUN git clone -b release/v3.3 --depth 1 --recursive https://github.com/espressif/esp-idf.git $IDF_PATH \
    && cd $IDF_PATH && git submodule foreach --recursive 'git gc --aggressive --prune=all'
RUN python -m pip install --user -r $IDF_PATH/requirements.txt
RUN mkdir /root/cmake && cd /root/cmake && wget https://cmake.org/files/v3.7/cmake-3.7.2-Linux-x86_64.sh && chmod +x ./cmake-3.7.2-Linux-x86_64.sh && ./cmake-3.7.2-Linux-x86_64.sh --skip-license


