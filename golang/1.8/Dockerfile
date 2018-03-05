FROM golang:1.8
MAINTAINER leodotcloud@gmail.com

RUN apt-get update && apt-get install -y \
    build-essential \
    iproute2 \
    iptables \
    ipset \
    iputils-ping \
    psmisc \
    tcpdump \
    vim \
    net-tools \
    arping \
    conntrack \
    iperf \
    curl \
    wget \
    jq \
    iperf3 \
    bzip2 \
    ethtool \
    openssl

RUN cd /tmp && \
    wget https://get.docker.com/builds/Linux/x86_64/docker-1.12.6.tgz && \
    tar xvfz docker*.tgz && \
    mv docker/* /usr/bin/ && \
    rm -rf docker && \
    wget https://github.com/aktau/github-release/releases/download/v0.7.2/linux-amd64-github-release.tar.bz2 && \
    tar xvfj linux-amd64-github-release.tar.bz2 && \
    mv bin/linux/amd64/github-release /usr/bin/ && \
    rm -rf bin

RUN mv /usr/sbin/tcpdump /usr/bin/tcpdump
ADD set_ps1.sh /tmp/set_ps1.sh
RUN cat /tmp/set_ps1.sh >> /root/.bashrc && rm /tmp/set_ps1.sh
