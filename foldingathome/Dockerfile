ARG BUILD_FROM=hassioaddons/debian-base:3.2.0
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Setup base system
ARG BUILD_ARCH=amd64
RUN \
    curl -J -L -o /tmp/fah.deb \
        "https://download.foldingathome.org/releases/public/release/fahclient/debian-stable-64bit/v7.6/fahclient_7.6.13_amd64.deb" \
    \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        bzip2=1.0.6-9.2~deb10u1 \
        ocl-icd-libopencl1=2.2.12-2 \
    \
    && mkdir /etc/fahclient \
    && touch /etc/fahclient/config.xml \
    && dpkg --install /tmp/fah.deb \
    \
    && rm -fr \
        /etc/fahclient \
        /tmp/* \
        /var/{cache,log}/* \
        /var/lib/apt/lists/*

# Copy root filesystem
COPY rootfs /

# Build arguments
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="Folding@home" \
    io.hass.description="Fighting disease with a world wide distributed super computer" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Franck Nijhof <frenck@addons.community>" \
    org.opencontainers.image.title="Folding@home" \
    org.opencontainers.image.description="Fighting disease with a world wide distributed super computer" \
    org.opencontainers.image.vendor="Home Assistant Community Add-ons" \
    org.opencontainers.image.authors="Franck Nijhof <frenck@addons.community>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://addons.community" \
    org.opencontainers.image.source="https://github.com/hassio-addons/addon-foldingathome" \
    org.opencontainers.image.documentation="https://github.com/hassio-addons/addon-foldingathome/blob/master/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
