# Copyright (c) Virtlog LLC.
# Distributed under the terms of the Modified BSD License.
ARG OWNER=virtlog
ARG BASE_CONTAINER=$OWNER/sage-notebook
FROM $BASE_CONTAINER

LABEL maintainer="Qin Li <li@virtlog.com>"

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

USER root

# Sage pre-requisites and jq for manipulating json
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    cmake \
    build-essential && \
    rm -rf /var/lib/apt/lists/*


USER $NB_UID

# Install rust evcxr_jupyter https://github.com/google/evcxr/tree/main/evcxr_jupyter
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y && \
    source $HOME/.cargo/env && \
    rustup component add rust-src && \
    cargo install evcxr_jupyter && \
    evcxr_jupyter --install && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER

ENV PATH="$HOME/.cargo/bin:${PATH}"