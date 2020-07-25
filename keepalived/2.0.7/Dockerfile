FROM alpine:3.12

# 维护者信息
LABEL maintainer="408093957@qq.com"

# Keepalived version
ARG KEEPALIVED_VERSION=2.0.7

RUN apk update \
    apk add --no-cache \
    autoconf \
    curl \
    gcc \
    ipset \
    ipset-dev \
    iptables \
    iptables-dev \
    libnfnetlink \
    libnfnetlink-dev \
    libnl3 \
    libnl3-dev \
    make \
    musl-dev \
    openssl \
    openssl-dev \
    tzdata \
	&& ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
	&& curl -o keepalived.tar.gz -SL http://keepalived.org/software/keepalived-${KEEPALIVED_VERSION}.tar.gz \
    && tar -xzf keepalived.tar.gz \
	&& cd keepalived \
	&& ./configure --disable-dynamic-linking \
    && make && make install \
	&& cd - && mkdir -p /etc/keepalived \
	#keepalived 启动脚本变量引用文件，默认文件路径是 /etc/sysconfig/，也可以不做软链接，直接修改启动脚本中文件路径即可（安装目录下）
	&& cp /usr/local/keepalived/etc/sysconfig/keepalived  /etc/sysconfig/keepalived \
	#将keepalived 主程序加入到环境变量（安装目录下）
	&& cp /usr/local/keepalived/sbin/keepalived /usr/sbin/keepalived \
	#keepalived 启动脚本（源码目录下），放到 /etc/init.d/ 目录下就可以使用 service 命令便捷调用
	&& cp keepalived/etc/init.d/keepalived  /etc/init.d/keepalived \
	#将配置文件放到默认路径下
	&& cp /usr/local/keepalived/etc/keepalived/keepalived.conf /etc/keepalived/keepalived.conf \
	&& rm -f keepalived.tar.gz \
    && rm -rf /keepalived \
    && rm /var/cache/apk/* \
    && apk --no-cache del \
	autoconf \
    gcc \
    ipset-dev \
    iptables-dev \
    libnfnetlink-dev \
    libnl3-dev \
    make \
    musl-dev \
    openssl-dev \
	tzdata

#挂载配置文件
VOLUME 	/etc/keepalived

#启动keepalived
ENTRYPOINT ["service","keepalived","start"]