FROM ubuntu:xenial
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

ENV GOLANG_VERSION 1.11

RUN cd /tmp && \
    wget https://get.docker.com/builds/Linux/x86_64/docker-1.12.6.tgz && \
    tar xvfz docker*.tgz && \
    mv docker/* /usr/bin/ && \
    rm -rf docker && \
    wget https://github.com/aktau/github-release/releases/download/v0.7.2/linux-amd64-github-release.tar.bz2 && \
    tar xvfj linux-amd64-github-release.tar.bz2 && \
    mv bin/linux/amd64/github-release /usr/bin/ && \
    rm -rf bin

RUN curl -L https://github.com/docker/machine/releases/download/v0.13.0/docker-machine-`uname -s`-`uname -m` > /tmp/docker-machine && \
    install /tmp/docker-machine /usr/local/bin/docker-machine

RUN curl -L https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl > /tmp/kubectl && \
    install /tmp/kubectl /usr/local/bin/kubectl

RUN cd /tmp && \
	wget https://dl.google.com/go/go${GOLANG_VERSION}.linux-amd64.tar.gz && \
	tar -C /usr/local -xzf go${GOLANG_VERSION}.linux-amd64.tar.gz && \
	rm -f go${GOLANG_VERSION}.linux-amd64.tar.gz

ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"
WORKDIR $GOPATH

RUN mv /usr/sbin/tcpdump /usr/bin/tcpdump
ADD set_ps1.sh /tmp/set_ps1.sh
RUN cat /tmp/set_ps1.sh >> /root/.bashrc && rm /tmp/set_ps1.sh
