FROM debian:latest
WORKDIR /render

RUN apt-get -qq update \
  && apt-get -qq install --upgrade -y --no-install-recommends \
    apt-transport-https \
    ca-certificates \
    netcat \
    wget \
    dnsutils \
  > /dev/null \
  && apt-get -qq clean \
  && rm -rf \
    /var/lib/apt/lists/* \
    /tmp/* \
    /var/tmp/* \
  && :

RUN echo "+search +short" > /root/.digrc
COPY tailscale/run-tailscale.sh tailscale/start.sh /render/

COPY tailscale/install-tailscale.sh /tmp
RUN /tmp/install-tailscale.sh && rm -r /tmp/*

CMD ./start.sh