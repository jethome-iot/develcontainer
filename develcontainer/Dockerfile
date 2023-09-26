FROM --platform=$BUILDPLATFORM ubuntu:jammy AS build
ARG TARGETPLATFORM
ARG BUILDPLATFORM

# renovate: datasource=github-releases depName=Kitware/CMake
ARG CMAKE_VERSION=3.27.4
ARG GCC_VERSION=10

RUN apt update \
      && apt install -y --no-install-recommends \
      wget build-essential make libgpiod-dev libgpiod2 gdb gdbserver libusb-dev libusb-1.0-0-dev usbutils git ca-certificates \
      && apt clean \
      && rm -rf /var/lib/apt/lists/*

RUN export BUILD_ARCH="$(uname -m)" && if [ "${BUILD_ARCH}" = "aarch64" ]; then \
          echo "Selected aarch64"; \
          wget https://github.com/Kitware/CMake/releases/download/v${CMAKE_VERSION}/cmake-${CMAKE_VERSION}-linux-aarch64.sh --no-check-certificate -O /tmp/cmake-install.sh ; \
      else \
          echo "Selected x86_64"; \
          wget https://github.com/Kitware/CMake/releases/download/v${CMAKE_VERSION}/cmake-${CMAKE_VERSION}-linux-x86_64.sh --no-check-certificate -O /tmp/cmake-install.sh ; \
      fi \
      && chmod u+x /tmp/cmake-install.sh \
      && mkdir /usr/bin/cmake \
      && /tmp/cmake-install.sh --skip-license --prefix=/usr \
      && rm /tmp/cmake-install.sh
