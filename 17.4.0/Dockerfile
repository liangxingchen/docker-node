FROM node:17.4.0-bullseye-slim

RUN echo "Asia/Shanghai" > /etc/timezone

ENV TZ=Asia/Shanghai
ENV NPM_CONFIG_REGISTRY=https://registry.npm.taobao.org/

COPY sources.list /etc/apt/sources.list

RUN apt-get update \
&& apt-get install -y --no-install-recommends ca-certificates bzip2 \
&& rm -rf /var/lib/apt/lists/*

