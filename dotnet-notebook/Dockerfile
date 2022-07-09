# Copyright (c) Virtlog LLC.
# Distributed under the terms of the Modified BSD License.
ARG OWNER=virtlog
ARG BASE_CONTAINER=$OWNER/rust-notebook
FROM $BASE_CONTAINER

LABEL maintainer="Qin Li <li@virtlog.com>"

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

USER root

# dotnet pre-requisites
RUN wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb && \
    dpkg -i packages-microsoft-prod.deb && \
    rm packages-microsoft-prod.deb

# install dotnet and dotnet-interactive
# Official https://github.com/dotnet/interactive
# New https://developers.refinitiv.com/en/article-catalog/article/using--net-core-in-jupyter-notebook
# Old https://devblogs.microsoft.com/dotnet/net-core-with-juypter-notebooks-is-here-preview-1/
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    apt-transport-https \
    dotnet-sdk-6.0 && \
    dotnet tool install --global Microsoft.dotnet-interactive && \
    rm -rf /var/lib/apt/lists/*

ENV PATH="$HOME/.dotnet/tools:${PATH}"

RUN dotnet-interactive jupyter install

USER $NB_UID
