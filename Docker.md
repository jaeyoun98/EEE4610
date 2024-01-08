# Generating Docker image (dockerfile code)
```
# Docker image: ubuntu:18.04
FROM accelsim/ubuntu-18.04_cuda-11

# Hi! I am...
MAINTAINER jyoon9811@yonsei.ac.kr

# Basic settings
RUN apt-get -y -qq update
RUN apt-get install -y git vim wget curl sudo

# Install python3.8, pip
RUN apt-get install -y software-properties-common python3.8 python3.8-distutils; cd ~; curl -O https://bootstrap.pypa.io/get-pip.py; python3.8 get-pip.py

# Install cuda 11.3.0
RUN wget https://developer.download.nvidia.com/compute/cuda/11.3.0/local_installers/cuda_11.3.0_465.19.01_linux.run
RUN sh cuda_11.3.0_465.19.01_linux.run --silent --toolkit

# Install PyTorch (1.12.1)
RUN pip install torch==1.12.1+cu113 torchvision==0.13.1+cu113 torchaudio==0.12.1 --extra-index-url https://download.pytorch.org/whl/cu113;

# Install PyG (2.0.3)
# RUN pip install torch-geometric==2.0.3
# RUN pip install --no-index torch_scatter torch_sparse torch_cluster torch_spline_conv -f https://data.pyg.org/whl/torch-1.10.1+cu111.html

# Install DGL (1.1.1)
# RUN pip install dgl --no-index -f https://data.dgl.ai/wheels/cu113/repo.html
# RUN pip install dglgo -f https://data.dgl.ai/wheels-test/repo.html

RUN apt-get -y -qq update

# Install python libraries
RUN pip install pyyaml

# python3 linking
RUN update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.8 1
RUN update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 0

WORKDIR /EEE4610/

# Install Accel-Sim
RUN git clone --branch dev --single-branch https://github.com/accel-sim/accel-sim-framework
```

# Build container
```
docker build -t [이미지] [컨테이너 위치]
docker build -t accel-sim/ubuntu-18.04_3.8_11.3.0_1.12.1 .
```

# Run container
```
docker run -it --name=jykim --gpus all --restart=unless-stopped -v /home/jykim/share:/EEE4610/share accel-sim/ubuntu-18.04_3.8_11.3.0_1.12.1 /bin/bash
```
컨테이너 환경과 로컬 환경을 mount할 수 있다 (파일 공유).

# Attach to container
```
docker attach [컨테이너이름]
```

# Container exit
```
ctrl + d : 종료
ctrl + p + q: 중단없이 나가기
```
