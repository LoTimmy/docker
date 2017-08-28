FROM ubuntu:16.04

RUN apt-get update -qq \
    && DEBIAN_FRONTEND=noninteractive apt-get -qq -y --no-install-recommends install ca-certificates wget \
    && rm -rf /var/lib/apt/lists/*

RUN wget -q --content-disposition https://minergate.com/download/deb-cli \
    && dpkg -i *.deb \
    && rm *.deb

ENTRYPOINT ["minergate-cli"]
