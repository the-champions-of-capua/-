FROM  debian:buster
MAINTAINER actanble <actanble@gmail.com>

RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak && \
cat > /etc/apt/sources.list <<- EOF
deb http://mirrors.ustc.edu.cn/debian buster main contrib non-free
deb-src http://mirrors.ustc.edu.cn/debian buster main contrib non-free
deb http://mirrors.ustc.edu.cn/debian buster-proposed-updates main contrib non-free
deb-src http://mirrors.ustc.edu.cn/debian buster-proposed-updates main contrib non-free
deb http://mirrors.ustc.edu.cn/debian buster-updates main contrib non-free
deb-src http://mirrors.ustc.edu.cn/debian buster-updates main contrib non-free
deb-src http://mirrors.ustc.edu.cn/debian sid main contrib non-free
EOF

## 安装所有的通用安装包
RUN apt-get update -qq && apt-get install build-essential libexpat1-dev libgeoip-dev \
libpng-dev libpcre3-dev libssl-dev libxml2-dev rcs \
zlib1g-dev libmcrypt-dev libcurl4-openssl-dev \
libjpeg-dev libpng-dev libwebp-dev pkg-config -y

RUN apt-get update -qq && apt-get install libglib2.0-dev python3 python3-dev
RUN apt-get update -qq && apt-get install -y wget gnupg2
RUN apt-get update -qq && apt-get install -y gcc make

EXPOSE 601/tcp

WORKDIR /spool/syslog-ng/

RUN wget https://github.com/balabit/syslog-ng/releases/download/syslog-ng-3.20.1/syslog-ng-3.20.1.tar.gz && \
tar zxvf syslog-ng-3.20.1.tar.gz && cd syslog-ng-3.20.1 && \
./configure --prefix=/spool/syslog-ng --enable-ipv6 --enable-python --with-python=3

RUN echo 'export PYTHONPATH=$PYTHONPATH:/etc/syslog-ng/zxsyslog/' | /bin/bash

ENTRYPOINT ["/spool/syslog-ng/sbin/syslog-ng", "-F"]
