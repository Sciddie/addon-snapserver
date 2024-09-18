ARG BUILD_FROM=ghcr.io/hassio-addons/base:16.3.1
FROM $BUILD_FROM

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

ARG LIBRESPOT_VERSION="0.4.2"
# hadolint ignore=DL3003
RUN \
    apk add --no-cache --virtual .build-dependencies \
        build-base \
        cargo \
        git \
        protobuf-dev \
        pulseaudio-dev \
    \
    && apk add --no-cache \
        pulseaudio \
    \
    && apk add --no-cache \
        librespot \
        --repository=https://dl-cdn.alpinelinux.org/alpine/edge/testing \
    && apk del --no-cache --purge .build-dependencies \
    && rm -fr \
        /tmp/* \
        ~/.cargo \
        /usr/.crates.toml \
        /usr/.crates2.json

#Install Snapcast
RUN apk add --no-cache snapcast-server bash

# Copy data for add-on
COPY run.sh /
RUN chmod a+x /run.sh

CMD [ "/run.sh" ]
