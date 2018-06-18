FROM ubuntu:16.04
LABEL maintainer "hyperloris"

ARG BUILD_DEPS=" \
    build-essential \
    ca-certificates \
    cmake \
    git \
    libhwloc-dev \
    libmicrohttpd-dev \
    libssl-dev "

RUN apt-get update && apt-get install -y --no-install-recommends \
    ${BUILD_DEPS} \
&& rm -rf /var/lib/apt/lists/*

WORKDIR /tmp

RUN git clone https://github.com/fireice-uk/xmr-stak-cpu.git \
    && cd xmr-stak-cpu/ \
    && cmake . \
    && make install \
    && cp bin/* /root/

RUN apt-get remove -y ${BUILD_DEPS}
RUN rm -rf /tmp/*

WORKDIR /root

ENTRYPOINT ["./xmr-stak-cpu"]
