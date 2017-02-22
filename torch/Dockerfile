FROM kaixhin/cuda-torch

MAINTAINER Alexander Sologub <alexander.sologub@altoros.com>

RUN git clone https://github.com/facebookresearch/deepmask && \
    cp -R deepmask/. /root/torch && \
    rm -rf deepmask

RUN apt-get install -y wget && \
    mkdir -p /root/torch/pretrained/deepmask && \
    cd /root/torch/pretrained/deepmask && \
    wget https://s3.amazonaws.com/deepmask/models/deepmask/model.t7 && \
    mkdir -p /root/torch/pretrained/sharpmask && \
    cd /root/torch/pretrained/sharpmask && \
    wget https://s3.amazonaws.com/deepmask/models/sharpmask/model.t7

# TODO AS: Torch itself?
# RUN luarocks install torch

# Coco
RUN luarocks install https://raw.githubusercontent.com/pdollar/coco/master/LuaAPI/rocks/coco-scm-1.rockspec

# Image
RUN luarocks install image

# TDS
RUN luarocks install tds

# Lua--JSON
RUN luarocks install json

# Lua--NNX
# https://github.com/clementfarabet/lua---nnx
# RUN luarocks install https://raw.githubusercontent.com/clementfarabet/lua---nnx/master/nnx-0.1-1.rockspec
RUN luarocks install nnx

# Optim
# https://github.com/torch/optim
# RUN luarocks install https://raw.githubusercontent.com/clementfarabet/lua---nnx/master/nnx-0.1-1.rockspec
RUN luarocks install optim

# Cutorch
# https://github.com/torch/cutorch
# RUN luarocks install cutorch 1.0-0
# RUN luarocks install cutorch

# Cunn
# https://github.com/torch/cunn
# RUN luarocks install cunn

# Imagine NN
# https://github.com/szagoruyko/imagine-nn
RUN luarocks install inn

# Cunn-torch
# https://github.com/soumith/cudnn.torch
# RUN luarocks install cudnn
