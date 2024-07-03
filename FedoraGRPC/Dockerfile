FROM fedora:41

RUN dnf update -y && dnf install -y \
    autoconf \
    automake \
    cmake \
    curl \
    g++ \
    git \
    libtool \
    make \
    pkg-config \
    unzip  \
    sudo

ENV GRPC_RELEASE_TAG v1.65.0
ENV GRPC_INSTALL_DIR /var/local/git/grpc/InstalledGRPC
ENV GRPC_INCLUDE_DIR ${GRPC_INSTALL_DIR}/include

ENV gRPC_DIR ${GRPC_INSTALL_DIR}/lib/cmake/grpc
ENV absl_DIR ${GRPC_INSTALL_DIR}/lib64/cmake/absl
ENV protobuf_DIR ${GRPC_INSTALL_DIR}/lib64/cmake/protobuf
ENV c-ares_DIR ${GRPC_INSTALL_DIR}/lib64/cmake/c-ares
ENV re2_DIR ${GRPC_INSTALL_DIR}/lib64/cmake/re2
ENV utf8_range_DIR ${GRPC_INSTALL_DIR}/lib64/cmake/utf8_range
ENV CMAKE_EXPORT_COMPILE_COMMANDS=ON

RUN git clone --recurse-submodules -b ${GRPC_RELEASE_TAG} --depth 1 https://github.com/grpc/grpc /var/local/git/grpc

RUN echo "-- Build GRPC With submodules and Install" && \
    cd /var/local/git/grpc && \
    mkdir -p cmake/build && \
    mkdir -p Installed && \
    pushd cmake/build && \
    cmake -DgRPC_INSTALL=ON \
      -DgRPC_BUILD_TESTS=OFF \
      -DCMAKE_INSTALL_PREFIX=$GRPC_INSTALL_DIR \
      ../.. && \
    make -j 4 && \
    make install && \
    popd

RUN echo "-- GRPC and third-party install to $GRPC_INSTALL_DIR"

ENV WORK_USERNAME Developer
ENV WORK_USERPASS DeveloperPassword

RUN useradd -ms /bin/bash ${WORK_USERNAME}

RUN echo "${WORK_USERNAME}:${WORK_USERPASS}" | chpasswd

ENV WORK_USERPASS ""

RUN usermod -aG wheel ${WORK_USERNAME}

USER ${WORK_USERNAME}
