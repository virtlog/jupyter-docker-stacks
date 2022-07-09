# Copyright (c) Virtlog LLC.
# Distributed under the terms of the Modified BSD License.
ARG OWNER=virtlog
ARG BASE_CONTAINER=$OWNER/all-spark-notebook
FROM $BASE_CONTAINER

LABEL maintainer="Qin Li <li@virtlog.com>"

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Install SageMath
ARG SAGE_VERSION=9.5
ARG SAGE_PYTHON_VERSION=3.10

USER root

# Sage pre-requisites and jq for manipulating json
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    dvipng \
    ffmpeg \
    imagemagick \
    texlive \
    tk tk-dev \
    jq && \
    rm -rf /var/lib/apt/lists/*


USER $NB_UID

# Install Sage conda environment
RUN conda init bash && \
    conda create --quiet --yes -n sage -c conda-forge sage=$SAGE_VERSION python && \
    conda clean --all -f -y && \
    npm cache clean --force

RUN ln -s /opt/conda/envs/sage/share/jupyter/kernels/python3 /opt/conda/share/jupyter/kernels/python3-sage && \
    ln -s /opt/conda/envs/sage/share/jupyter/kernels/sagemath /opt/conda/share/jupyter/kernels/sagemath && \
    sed -i "s/(ipykernel)/(sage)/" /opt/conda/share/jupyter/kernels/python3-sage/kernel.json && \
    mkdir $HOME/.sage && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER
