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

RUN luarocks install https://raw.githubusercontent.com/pdollar/coco/master/LuaAPI/rocks/coco-scm-1.rockspec && \
    luarocks install image && \
    luarocks install tds && \
    luarocks install json && \
    luarocks install nnx && \
    luarocks install optim && \
    luarocks install inn
