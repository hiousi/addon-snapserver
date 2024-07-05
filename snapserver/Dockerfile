ARG BUILD_FROM=ghcr.io/hassio-addons/base:16.1.2
FROM $BUILD_FROM

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Setup base
ARG SNAPCAST_VERSION="0.28.0-r2"
ARG LIBRESPOT_VERSION="0.4.2-r4"
ARG SNAPWEB_VERSION="0.7.0"

RUN \
    apk add --no-cache \
        pulseaudio bash \
    && rm -fr \
        /tmp/*

RUN apk add --no-cache --repository=http://dl-cdn.alpinelinux.org/alpine/edge/community/ snapcast-server=${SNAPCAST_VERSION}

RUN apk add --no-cache --repository=http://dl-cdn.alpinelinux.org/alpine/edge/testing/ librespot=${LIBRESPOT_VERSION}

RUN \
    wget https://github.com/badaix/snapweb/releases/download/v${SNAPWEB_VERSION}/snapweb.zip && \
    unzip -o snapweb.zip -d /usr/share/snapserver/snapweb/ && \
    rm snapweb.zip

# Copy data for add-on
COPY run.sh /
RUN chmod a+x /run.sh



CMD [ "/run.sh" ]
