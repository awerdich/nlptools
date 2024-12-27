FROM nvcr.io/nvidia/pytorch:24.11-py3 AS base
# https://catalog.ngc.nvidia.com/orgs/nvidia/containers/pytorch/tags
# Python 3.10.12

ARG DEV_nlptools

ENV \
    PYTHONDONTWRITEBYTECODE=1 \
    PYTHONFAULTHANDLER=1 \
    PYTHONUNBUFFERED=1 \
    PYTHONHASHSEED=random \
    PIP_NO_CACHE_DIR=off \
    PIP_DISABLE_PIP_VERSION_CHECK=on \
    PIP_DEFAULT_TIMEOUT=100 \
    PIP_SRC=/src \
    PIPENV_HIDE_EMOJIS=true \
    NO_COLOR=true \
    PIPENV_NOSPIN=true

# Port for JupyterLab server
EXPOSE 8888

RUN mkdir -p /app
WORKDIR /app

# System dependencies
RUN apt-get update -y && \
    apt-get upgrade -y

# Pip
RUN pip install --upgrade pip
RUN pip install pipenv

# We need the setup package information
COPY setup.py ./
COPY src/nlptools/__init__.py src/nlptools/__init__.py

# Additional dependencies 
COPY Pipfile Pipfile.lock ./
RUN --mount=source=.git,target=.git,type=bind  \
    pipenv install --system --deploy --ignore-pipfile --dev
# Fix versions for packages defined in the .lock file
RUN --mount=source=.git,target=.git,type=bind  \
    pipenv sync --system

# Install the CUDA samples
RUN git clone https://github.com/NVIDIA/cuda-samples.git /opt/cuda-samples
RUN cd /opt/cuda-samples/Samples/1_Utilities/deviceQuery && \
    make && \
    cp  /opt/cuda-samples/Samples/1_Utilities/deviceQuery/deviceQuery /usr/local/bin

# Run the jupyter lab server
RUN mkdir -p /run_scripts
COPY /bash_scripts/docker_entry /run_scripts
RUN chmod +x /run_scripts/*
CMD ["/bin/bash", "/run_scripts/docker_entry"]