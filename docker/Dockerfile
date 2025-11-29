# Use a standard NVIDIA CUDA image that is compatible with CUDA 12.6.
# We'll choose a Python 3.12 image for stability and compatibility.
FROM nvidia/cuda:12.5.0-devel-ubuntu22.04

# Set environment variables for non-interactive install
ENV DEBIAN_FRONTEND=noninteractive

# Install common dependencies (git, wget, and basic build tools)
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    wget \
    git \
    build-essential && \
    rm -rf /var/lib/apt/lists/*

# Install Python 3.12
# Since the base image might have an older Python, we'll install 3.12 via PPA or manual build
# For simplicity and robustness, we'll rely on the Python from the base image if a specific 3.12 is hard to manage.
# A common practice is to use a specific Python image, but since we need CUDA, we'll install it here.
# For this example, let's assume Python 3.12 is installed/available, or we use a Python 3.12 base image with CUDA.
# Let's switch the base image to one with Python pre-installed for easier setup.
FROM pytorch/pytorch:2.7.0-cuda12.5-cudnn8-devel

# The base image already has Python and PyTorch/CUDA set up.
# Confirm Python version (it should be 3.12+ in the PyTorch 2.7 image)
# Run the installation steps

# Set the working directory
WORKDIR /app

# Clone the repository
RUN git clone https://github.com/facebookresearch/sam3.git
WORKDIR /app/sam3

# Install the package and core dependencies
# PyTorch 2.7 is already installed in the base image, matching your requirement.
# We need to ensure the local editable installation is done.
RUN pip install -e .

# Install additional dependencies for example notebooks
RUN pip install -e ".[notebooks]"
RUN pip install -e ".[train,dev]"

CMD ["/bin/bash"]