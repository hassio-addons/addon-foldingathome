ARG BUILD_FROM=hassioaddons/debian-base:3.0.1
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Setup base system
ARG BUILD_ARCH=amd64
RUN \
    curl -J -L -o /tmp/fah.deb \
        "https://download.foldingathome.org/releases/public/release/fahclient/debian-stable-64bit/v7.6/fahclient_7.6.9_amd64.deb" \
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
    io.hass.description="Fighting disease with a world wide distributed super computer." \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Franck Nijhof <frenck@addons.community>" \
    org.label-schema.description="Fighting disease with a world wide distributed super computer." \
    org.label-schema.build-date=${BUILD_DATE} \
    org.label-schema.name="Folding@home" \
    org.label-schema.schema-version="1.0" \
    org.label-schema.url="https://community.home-assistant.io/t/home-assistant-community-add-on-folding-home/180496?u=frenck" \
    org.label-schema.usage="https://github.com/hassio-addons/addon-foldingathome/tree/master/README.md" \
    org.label-schema.vcs-ref=${BUILD_REF} \
    org.label-schema.vcs-url="https://github.com/hassio-addons/addon-foldingathome" \
    org.label-schema.vendor="Home Assistant Community Add-ons"
