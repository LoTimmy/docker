AddedFROM ubuntu:16.04

ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update -qq \
    && apt-get -qq -y install cowsay \
    && apt-get -qq -y install fortunes \
    && rm -rf /var/lib/apt/lists/*

ENV PATH $PATH:/usr/games

CMD fortune -a | cowsay

