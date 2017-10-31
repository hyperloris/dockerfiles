FROM ubuntu:16.04
LABEL maintainer "hyperloris"

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    ca-certificates \
    cmake \
    git \
    g++ \
    python-dev \
    wget \
&& rm -rf /var/lib/apt/lists/*

WORKDIR /tmp

RUN wget -O boost_1_62_0.tar.gz https://sourceforge.net/projects/boost/files/boost/1.62.0/boost_1_62_0.tar.gz/download \
    && tar xzvf boost_1_62_0.tar.gz \
    && cd boost_1_62_0 \
    && ./bootstrap.sh --prefix=/usr/ \
    && n=`cat /proc/cpuinfo | grep "cpu cores" | uniq | awk '{print $NF}'` \
    && ./b2 -j $n \
    && ./b2 -j $n install

RUN git clone https://github.com/nicehash/nheqminer.git \
    && chmod +x nheqminer/cpu_xenoncat/asm_linux/* \
    && cd nheqminer/cpu_xenoncat/asm_linux/ \
    && sh assemble.sh \
    && cd ../../../ \
    && mkdir build \
    && cd build/ \
    && cmake -D USE_CUDA_DJEZO=OFF ../nheqminer \
    && make -j $(nproc) \
    && cp ./nheqminer /root/nheqminer

RUN rm -rf /tmp/*

WORKDIR /root

ENTRYPOINT ["./nheqminer"]
CMD ["-h"]