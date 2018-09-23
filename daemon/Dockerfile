FROM mhart/alpine-node:6.8

MAINTAINER Michael Parker, <docker@parkervcp.com>

WORKDIR /srv/daemon

RUN apk update \
 && apk add openssl make gcc g++ python linux-headers paxctl gnupg zip unzip git tar \
 && wget -qO- https://github.com/pterodactyl/daemon/releases/download/v0.6.5/daemon.tar.gz | tar xvz -C /srv/ \
 && mv /srv/daemon-*/* /srv/daemon \
 && npm install --production \
 && apk del curl make gcc g++ python linux-headers paxctl gnupg tar ${DEL_PKGS} \
 && rm -rf /node-${VERSION}.tar.gz /SHASUMS256.txt.asc /node-${VERSION} ${RM_DIRS} \
 /usr/share/man /tmp/* /var/cache/apk/* /root/.npm /root/.node-gyp /root/.gnupg \
 /usr/lib/node_modules/npm/man /usr/lib/node_modules/npm/doc /usr/lib/node_modules/npm/html

RUN addgroup -g 8888 -S pterodactyl
RUN adduser -u 8888 -S -D -H -G pterodactyl -s /bin/false pterodactyl

EXPOSE 8080

CMD ["npm", "start"]
