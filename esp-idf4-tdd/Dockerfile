# This dockerfile uses Environment for ESP32 CI builds
#
# Ubuntu 18.04
# https://hub.docker.com/_/ubuntu
#
# ESP-IDF v4.0
#
# adapted from https://hub.docker.com/r/larryli/esp-idf-ci-env/dockerfile
#

FROM ubuntu:18.04
MAINTAINER Todd Flanders todd.a.flanders@accenture.com

ENV IDF_PATH="/opt/local/espressif/esp-idf" 
ENV PATH="/opt/local/espressif/xtensa-esp32-elf/bin:/root/cmake/bin:${IDF_PATH}/tools:${PATH}"
ENV PATH="/opt/local/espressif/esp-idf/components/esptool_py/esptool:${PATH}"
ENV PATH="/opt/local/espressif/esp-idf/components/espcoredump:${PATH}"
ENV PATH="/opt/local/espressif/esp-idf/components/partition_table/:${PATH}"
ENV PATH="/root/.espressif/tools/xtensa-esp32-elf/esp-2019r2-8.2.0/xtensa-esp32-elf/bin:${PATH}"
ENV PATH="/root/.espressif/tools/esp32ulp-elf/2.28.51.20170517/esp32ulp-elf-binutils/bin:${PATH}"
ENV PATH="/root/.espressif/tools/openocd-esp32/v0.10.0-esp32-20190313/openocd-esp32/bin:${PATH}"
ENV PATH="/root/.espressif/python_env/idf4.0_py2.7_env/bin:${PATH}"

RUN apt-get update \
    && apt-get install -y gcc git wget make libncurses-dev \ 
       flex bison gperf python python-pip python-setuptools python-serial \ 
       python-cryptography python-future autoconf texinfo unzip help2man \ 
       gawk libtool libtool-bin libusb-1.0-0 \
	&& rm -r /var/lib/apt/lists/*
RUN mkdir -p /opt/local/espressif/ \
    && cd /opt/local/espressif/ \
    && git clone https://github.com/espressif/crosstool-NG.git \
    && cd crosstool-NG \
    && git checkout esp-2019r2 \
    && git submodule update --init \
    && ./bootstrap && ./configure --enable-local && make \
    && cd .. \
    && git clone -b release/v4.0 --depth 1 --recursive https://github.com/espressif/esp-idf.git $IDF_PATH

RUN python -m pip install --user -r $IDF_PATH/requirements.txt
RUN cd /opt/local/espressif/esp-idf && ./install.sh 
RUN mkdir /root/cmake && cd /root/cmake && wget https://cmake.org/files/v3.16/cmake-3.16.0-Linux-x86_64.sh && chmod +x ./cmake-3.16.0-Linux-x86_64.sh && ./cmake-3.16.0-Linux-x86_64.sh --skip-license
