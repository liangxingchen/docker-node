FROM alpine:3.12.1

MAINTAINER LiangXingchen <liang@maichong.it>

ENV NPM_CONFIG_LOGLEVEL=info \
  NPM_CONFIG_DISTURL=http://npm.taobao.org/mirrors/node \
  NPM_CONFIG_REGISTRY=https://registry.npm.taobao.org \
  NPM_CONFIG_PROGRESS=false \
  NPM_CONFIG_COLOR=false \
  NODE_VERSION=12.18.4 \
  YARN_VERSION=1.22.10

RUN apk add --update ca-certificates git curl make gcc g++ binutils-gold python linux-headers paxctl libgcc libstdc++ \
  && curl -sSL $NPM_CONFIG_DISTURL/v${NODE_VERSION}/node-v${NODE_VERSION}.tar.gz | tar -xz \
  && cd /node-v${NODE_VERSION} \
  && ./configure --prefix=/usr --fully-static \
  && make -j$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
  && make install \
  && paxctl -cm /usr/bin/node \
  && cd / \
  && if [ -x /usr/bin/npm ]; then \
    npm install -g npm \
    && find /usr/lib/node_modules/npm -name test -o -name .bin -type d | xargs rm -rf; \
  fi \
  && apk del curl make gcc g++ binutils-gold python linux-headers paxctl libgcc libstdc++ \
    openssl libssh2 ca-certificates binutils-libs binutils gmp isl libgomp libatomic pkgconf pkgconfig \
    mpfr3 mpc1 musl-dev libc-dev linux-headers paxctl libbz2 expat libffi gdbm ncurses-terminfo-base ncurses-terminfo \
    ncurses-libs readline sqlite-libs \
  && rm -rf /etc/ssl /node-v${NODE_VERSION} /usr/include \
    /root/.npm /root/.node-gyp \
    /usr/share/man /tmp/* /var/cache/apk/* \
    /usr/lib/node_modules/npm/man /usr/lib/node_modules/npm/doc /usr/lib/node_modules/npm/html \
  && curl -fSLO --compressed "https://yarnpkg.com/downloads/$YARN_VERSION/yarn-v$YARN_VERSION.tar.gz" \
  && tar -xzf yarn-v$YARN_VERSION.tar.gz -C /opt/ \
  && ln -s /opt/yarn-v$YARN_VERSION/bin/yarn /usr/local/bin/yarn \
  && ln -s /opt/yarn-v$YARN_VERSION/bin/yarnpkg /usr/local/bin/yarnpkg \
  && rm yarn-v$YARN_VERSION.tar.gz

CMD [ "node" ]
