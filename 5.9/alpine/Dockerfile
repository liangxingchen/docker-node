FROM alpine:3.3

MAINTAINER LiangXingchen <liang@maichong.it>

ENV NPM_CONFIG_LOGLEVEL=info \
  NPM_CONFIG_DISTURL=http://npm.taobao.org/mirrors/node \
  NPM_CONFIG_REGISTRY=https://registry.npm.taobao.org \
  NPM_CONFIG_PROGRESS=false \
  NPM_CONFIG_COLOR=false \
  NODE_VERSION=5.9.0

RUN apk add --update curl make gcc g++ binutils-gold python linux-headers paxctl libgcc libstdc++ \
  && curl -sSL $NPM_CONFIG_DISTURL/v${NODE_VERSION}/node-v${NODE_VERSION}.tar.gz | tar -xz \
  && cd /node-v${NODE_VERSION} \
  && ./configure --prefix=/usr --fully-static \
  && make -j$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
  && make install \
  && paxctl -cm /usr/bin/node \
  && cd / \
  && if [ -x /usr/bin/npm ]; then \
    npm install -g npm@${NPM_VERSION} \
    && find /usr/lib/node_modules/npm -name test -o -name .bin -type d | xargs rm -rf; \
  fi \
  && apk del curl make gcc g++ binutils-gold python linux-headers paxctl libgcc libstdc++ \
    openssl libssh2 ca-certificates binutils-libs binutils gmp isl libgomp libatomic pkgconf pkgconfig \
    mpfr3 mpc1 musl-dev libc-dev linux-headers paxctl libbz2 expat libffi gdbm ncurses-terminfo-base ncurses-terminfo \
    ncurses-libs readline sqlite-libs \
  && rm -rf /etc/ssl /node-v${NODE_VERSION} /usr/include \
    /usr/share/man /tmp/* /var/cache/apk/* /root/.npm /root/.node-gyp \
    /usr/lib/node_modules/npm/man /usr/lib/node_modules/npm/doc /usr/lib/node_modules/npm/html

CMD [ "node" ]
