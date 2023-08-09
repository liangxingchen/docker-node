FROM node:18.17.0-bookworm-slim

ENV TZ=Asia/Shanghai LANG=zh_CN.UTF-8 NPM_CONFIG_REGISTRY=https://registry.npmmirror.com/

COPY sources.list /etc/apt/sources.list

RUN echo "Asia/Shanghai" > /etc/timezone \
&& ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
&& apt-get update \
&& apt-get install -y --no-install-recommends locales ca-certificates curl iputils-ping telnet rsync procps pigz \
&& rm -rf /var/lib/apt/lists/* \
&& sed -ie 's/# zh_CN.UTF-8 UTF-8/zh_CN.UTF-8 UTF-8/g' /etc/locale.gen \
&& locale-gen

