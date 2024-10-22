# MIT License
# 
# Copyright (c) 2024 Rasmus Mikkelsen
# 
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
# 
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
# 
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.

FROM ubuntu:22.04

ARG HELM_VERSION=v3.14.2

ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Europe/Copenhagen

# Install APT packages
RUN \
    echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections && \
    apt-get update && \
    apt-get -y upgrade && \
    apt-get install -y --no-install-recommends \
        apt-transport-https \
        apt-utils \
        ca-certificates \
        curl \
        dnsutils \
        gnupg \
        iperf \
        iputils-ping \
        nano \
        net-tools \
        netcat \
        nmap \
        openssl \
        socat \
        sudo \
        telnet \
        tcpdump \
        traceroute \
        tzdata \
        wget \
        && \
    apt-get clean && \
    apt autoremove -y && \
    rm -rf /var/lib/{apt,dpkg,cache,log}/

# Set time zone
RUN \
    ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && \
    echo $TZ > /etc/timezone

# Install Helm
RUN \
    wget --quiet -O - https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash -s -- -v ${HELM_VERSION}

# Install kubectl
RUN \
    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl" && \
    chmod +x kubectl && \
    mv kubectl /usr/local/bin/kubectl

# Add a user
RUN \
    adduser \
        --disabled-password \
        --uid 1000 \
        --shell /bin/bash \
        debug \
        && \
    echo '%debug ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER debug
WORKDIR /home/debug

ENTRYPOINT ["tail", "-f", "/dev/null"]
