FROM nvidia/cuda:12.6.0-devel-ubuntu22.04

ENV DEBIAN_FRONTEND=noninteractive
ENV PATH="/root/.local/bin:${PATH}"

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    software-properties-common \
    build-essential \
    wget \
    git && \
    add-apt-repository ppa:deadsnakes/ppa && \
    apt-get update && \
    apt-get install -y python3.12 python3.12-venv && \
    update-alternatives --set python3 /usr/bin/python3.12 && \
    wget https://bootstrap.pypa.io/get-pip.py -O get-pip.py && \
    python3.12 get-pip.py && \
    rm get-pip.py && \
    rm -rf /var/lib/apt/lists/*

RUN pip install torch==2.7.0 torchvision torchaudio --index-url https://download.pytorch.org/whl/cu126

WORKDIR /app
RUN git clone https://github.com/facebookresearch/sam3.git
WORKDIR /app/sam3
RUN pip install -e .

RUN pip install -e ".[notebooks]"
RUN pip install -e ".[train,dev]"

CMD ["/bin/bash"]