# Copyright (c) Virtlog LLC.
# Distributed under the terms of the Modified BSD License.
ARG OWNER=virtlog
ARG BASE_CONTAINER=$OWNER/dotnet-notebook
FROM $BASE_CONTAINER

LABEL maintainer="Qin Li <li@virtlog.com>"

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

USER root

# Install https://github.com/jina-ai/discoart
RUN pip install jupyter_http_over_ws discoart && \
    jupyter nbextension enable --py widgetsnbextension && \
    jupyter serverextension enable --py jupyter_http_over_ws

USER $NB_UID
