#ARG GCC_VERSION=10
#FROM gcc:$GCC_VERSION
FROM --platform=$BUILDPLATFORM ubuntu:jammy AS build
ARG TARGETPLATFORM
ARG BUILDPLATFORM



FROM ubuntu

# renovate: datasource=github-releases depName=Kitware/CMake
ARG CMAKE_VERSION=3.27.4

RUN apt update \
      && apt install -y --no-install-recommends \
      wget build-essential make \
      && apt clean \
      && rm -rf /var/lib/apt/lists/*

RUN wget https://github.com/Kitware/CMake/releases/download/v${CMAKE_VERSION}/cmake-${CMAKE_VERSION}-Linux-x86_64.sh --no-check-certificate -O /tmp/cmake-install.sh \
      && chmod u+x /tmp/cmake-install.sh \
      && mkdir /usr/bin/cmake \
      && /tmp/cmake-install.sh --skip-license --prefix=/usr/bin/cmake \
      && rm /tmp/cmake-install.sh

ENV PATH="/usr/bin/cmake/bin:${PATH}"