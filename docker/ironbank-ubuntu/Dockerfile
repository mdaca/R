# Stage 1: Build R from source
ARG BASE_REGISTRY=201959883603.dkr.ecr.us-east-2.amazonaws.com
ARG BASE_IMAGE_PATH=mdaca/base-images/ironbank-ubuntu
ARG BASE_TAG=22.04_stable
ARG BASE_IMAGE=${BASE_REGISTRY}/${BASE_IMAGE_PATH}:${BASE_TAG}
FROM $BASE_IMAGE AS build-r

# Set environment variables
ENV R_VERSION=4.4.1
ENV R_HOME=/usr/local/lib/R
ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=America/New_York

# Install required dependencies
RUN apt-get update -y && \
    apt-get install -y build-essential gfortran libreadline-dev libx11-dev libxt-dev \
    libpng-dev libjpeg-dev libcairo2-dev libbz2-dev liblzma-dev libpcre2-dev \
    libcurl4-openssl-dev libssl-dev texinfo texlive texlive-fonts-extra \
    texlive-fonts-recommended texlive-latex-extra libxml2-dev libsqlite3-dev \
    zlib1g-dev libtiff5-dev libtiff-tools libblas-dev liblapack-dev wget openjdk-11-jdk &&  \
    rm -rf /var/lib/apt/lists/*

# Download and extract R source code
RUN wget https://cran.r-project.org/src/base/R-4/R-${R_VERSION}.tar.gz && \
    tar -xzf R-${R_VERSION}.tar.gz && \
    cd R-${R_VERSION} && \
    ./configure --enable-R-shlib --with-blas --with-lapack && \
    make -j$(nproc) && \
    make install && R --version

