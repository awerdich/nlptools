[![Pyscaffold](https://img.shields.io/badge/-PyScaffold-005CA0?logo=pyscaffold)](
https://pyscaffold.org/)
[![Python 3.12](
https://img.shields.io/badge/python-3.12-blue.svg)](
https://www.python.org/downloads/release/python-3123/)
[![docker](
https://github.com/ccb-hms/computervision/actions/workflows/docker.yml/badge.svg?branch=develop)](
https://github.com/ccb-hms/computervision/actions/workflows/docker.yml)

<p float="left">
    <img style="vertical-align: top" src="./images/OSS-Nvidia-Partnership-Pytorch.webp" width="40%" />
</p>

## The PyTorch NLP Tools Repository ##

This repository contains template code that that can be used as a starting point for NLP projects. 
All frameworks, libraries and data sets are open source and publicly available.
The software stack includes

- Python 3.12.3
- PyTorch 2.6.0
- CUDA
- cuBLAS
- NVIDIA cuDNN
- NVIDIA NCCL (optimized for NVLink)
- RAPIDS
- NVIDIA Data Loading Library (DALI)
- TensorRT
- Torch-TensorRT

## Install locally with Docker
The most convenient way to get started with this repository is to run the 
code examples in a [Docker](https://docs.docker.com/) container.

The Dockerfile and docker-compose.yml included in the repository contain the instructions
to create a Docker image and run a Docker container, which together provide a 
reproducible Python development environment. This environment is based on Ubuntu 24.04.01 LTS and contains
everything needed to get started prototyping NLP methods with the latest 
open-source LLM models. I have also included a Jupyter Lab server, 
making this repository it well-suited for training and evaluating custom models.

Here's a step-by-step guide on how to use this setup:

1. Install [Docker](https://docs.docker.com/) on your machine.
2. Clone the GitHub project repository to download the contents of the repository:
```bash
git clone git@github.com:awerdich/nlptools.git
```
3. Navigate to the repository's directory: Use `cd nlptools` to change your current directory to the repository's 
directory.
4. Build the Docker image. Use the command `docker compose build` to build a Docker image from the 
Dockerfile in the current directory. This image will include all the specifications from the Dockerfile, 
such as Ubuntu 24.04, Python 3.12, PyTorch 2.6 with CUDA, and a Jupyter Lab server.
5. Run `docker compose up` to start the Docker container based on the configurations 
in the docker-compose.yml file. 
The default `docker-compose.yml`file expects a GPU accelerator 
and the NVIDIA Container Toolkit installed on the local machine.
Without a GPU, training of the neural networks in the example notebooks will be extremely slow.
6. Access Jupyter Lab: Click on the link that starts with `localhost:8888` provided by the 
output of the last command.

### GPU support for Docker ###

The NVIDIA Container Toolkit is a set of tools designed to enable GPU-accelerated applications to run within Docker containers. 
This toolkit facilitates the integration of NVIDIA GPUs with container runtimes, 
allowing developers and data scientists to harness the power of GPU computing in containerized environments.
See the [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html) page for installation instructions.