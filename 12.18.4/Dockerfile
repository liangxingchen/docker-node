FROM maichong/ubuntu:18.04

ENV NPM_CONFIG_LOGLEVEL=http \
  NPM_CONFIG_DISTURL=http://npm.taobao.org/mirrors/node \
  NPM_CONFIG_PROGRESS=false \
  NPM_CONFIG_COLOR=false \
  NODE_VERSION=12.18.4 \
  YARN_VERSION=1.22.10

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
  ca-certificates \
  curl \
  gcc \
  make \
  git \
  bzip2 \
  && curl -sSL $NPM_CONFIG_DISTURL/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-x64.tar.gz | tar -xz -C /usr/local --strip-components=1 \
  && find /usr/local/lib/node_modules/npm -name test -o -name .bin -o -name example -o -name examples -type d | xargs rm -rf \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  /root/.npm \
  /usr/share/man /tmp/* \
  /usr/local/lib/node_modules/npm/man /usr/local/lib/node_modules/npm/doc /usr/local/lib/node_modules/npm/html \
  && curl -fSLO --compressed "https://yarnpkg.com/downloads/$YARN_VERSION/yarn-v$YARN_VERSION.tar.gz" \
  && tar -xzf yarn-v$YARN_VERSION.tar.gz -C /opt/ \
  && ln -s /opt/yarn-v$YARN_VERSION/bin/yarn /usr/local/bin/yarn \
  && ln -s /opt/yarn-v$YARN_VERSION/bin/yarnpkg /usr/local/bin/yarnpkg \
  && rm yarn-v$YARN_VERSION.tar.gz

CMD [ "node" ]