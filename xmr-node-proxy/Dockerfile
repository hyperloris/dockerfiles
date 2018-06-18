FROM ubuntu:16.04
LABEL maintainer "lorenzo.dramis@gmail.com"

ARG BUILD_DEPS=" \
    build-essential \
    cmake \
    curl \
    git \
    pkg-config "

RUN apt-get update && apt-get install -y --no-install-recommends \
    ${BUILD_DEPS} \
    libboost-all-dev \
    libevent-dev \
    libexpat1-dev \
    libgtest-dev \
    libldns-dev \
    liblzma-dev \
    libminiupnpc-dev \
    libunbound-dev \
    libunwind8-dev \
    libzmq3-dev \
    ntp \
    python-virtualenv \
    python3-virtualenv \
    screen \
&& rm -rf /var/lib/apt/lists/*

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    && apt-get install -y nodejs

RUN git clone https://github.com/Snipa22/xmr-node-proxy \
    && cd xmr-node-proxy/ \
    && npm install \
    && cp config_example.json config.json \
    && openssl req -subj "/C=IT/ST=Pool/L=Daemon/O=Mining Pool/CN=mining.proxy" \
       -newkey rsa:2048 -nodes -keyout cert.key -x509 -out cert.pem -days 36500 \
    && apt-get remove -y ${BUILD_DEPS}

WORKDIR /xmr-node-proxy
ENTRYPOINT ["node","proxy.js"]