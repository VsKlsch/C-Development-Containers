FROM fedora:41

ENV WORK_USERNAME=developer
ENV WORK_USERPASS=developer

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
    sudo \
    tar \
    zip

RUN echo "Username: ${WORK_USERNAME}"

RUN useradd -ms /bin/bash ${WORK_USERNAME}

RUN echo "${WORK_USERNAME}:${WORK_USERPASS}" | chpasswd

RUN usermod -aG wheel ${WORK_USERNAME}

USER ${WORK_USERNAME}

WORKDIR /home/${WORK_USERNAME}

RUN git clone https://github.com/microsoft/vcpkg.git

WORKDIR /home/${WORK_USERNAME}/vcpkg

RUN ./bootstrap-vcpkg.sh --disableMetrics

ENV HOME=/home/${WORK_USERNAME}
ENV VCPKG_ROOT=${HOME}/vcpkg
ENV VCPKG_CMAKE=${VCPKG_ROOT}/scripts/buildsystems/vcpkg.cmake
ENV WORK_USERPASS=""

RUN echo 'export PATH=$PATH:$VCPKG_ROOT' >> ${HOME}/.bashrc
WORKDIR ${HOME}