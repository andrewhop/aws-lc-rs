ARG CROSS_BASE_IMAGE=ubuntu:20.04
FROM $CROSS_BASE_IMAGE

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install --assume-yes --no-install-recommends gpg-agent software-properties-common && \
    add-apt-repository --yes ppa:longsleep/golang-backports && \
    apt-get update && \
    apt-get install --assume-yes --no-install-recommends build-essential cmake golang-go clang && \
    git config --global --add safe.directory '*' && \
    rm -rf /tmp/*

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y --profile minimal --default-toolchain stable && \
    . $HOME/.cargo/env && \
    cargo install --force --locked bindgen-cli && \
    mv $HOME/.cargo/bin/bindgen /usr/bin && \
    rm -rf $HOME/.cargo

ENV GOCACHE=/tmp
