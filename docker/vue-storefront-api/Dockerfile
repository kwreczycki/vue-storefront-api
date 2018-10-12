FROM node:8-alpine

ENV VS_ENV dev

WORKDIR /var/www

RUN apk add --no-cache curl

COPY package.json ./

RUN apk update && apk upgrade && \
    apk add python3 && \
    ln -sf `which python3` /usr/bin/python && \
    apk add --virtual=build-dependencies curl && \
    curl https://bootstrap.pypa.io/get-pip.py | python3 && \
    apk del build-dependencies && \
    rm -Rf /root/.cache && \
    rm -rf /var/cache/apk/*

RUN apk add --no-cache --virtual .build-deps ca-certificates wget git && \
    yarn install --no-cache && \
    apk del .build-deps

COPY docker/vue-storefront-api/vue-storefront-api.sh /usr/local/bin/

CMD ["vue-storefront-api.sh"]
