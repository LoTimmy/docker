FROM ubuntu:16.04
ARG DEBIAN_FRONTEND=noninteractive

RUN set -ex; \
    \
    apt-get update; \
    apt-get install -y --no-install-recommends libmicrohttpd10 libssl1.0.0; \
    apt-get install -y tzdata; \
    echo "Asia/Taipei" > /etc/timezone; \
    dpkg-reconfigure -f noninteractive tzdata; \
    rm -rf /var/lib/apt/lists/*; 

RUN set -ex; \
    \
    fetchDeps='ca-certificates wget curl g++ libmicrohttpd-dev libssl-dev make git'; \
    apt-get update; \
    apt-get install -y --no-install-recommends $fetchDeps; \
    rm -rf /var/lib/apt/lists/*; \
    curl -SL https://cmake.org/files/v3.8/cmake-3.8.2-Linux-x86_64.tar.gz \
    | tar --strip=1 -xzC /usr/local; \
    git clone https://github.com/fireice-uk/xmr-stak-cpu.git; \
    cd xmr-stak-cpu; \
    sed -i 's/constexpr double fDevDonationLevel.*/constexpr double fDevDonationLevel = 0.0;/' donate-level.h; \
#    cmake .; \
    cmake . -DHWLOC_ENABLE=OFF; \
    make -j$(nproc); \
    apt-get purge -y --auto-remove $fetchDeps

WORKDIR /xmr-stak-cpu

EXPOSE 62787
ENTRYPOINT ["bin/xmr-stak-cpu"]
CMD ["/conf/config.txt"]
