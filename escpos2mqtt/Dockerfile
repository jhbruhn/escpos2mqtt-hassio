ARG BUILD_FROM

FROM ghcr.io/jhbruhn/escpos2mqtt:main AS escpos

# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
FROM ${BUILD_FROM}

# Execute during the build of the image
ARG TEMPIO_VERSION BUILD_ARCH
RUN \
    curl -sSLf -o /usr/bin/tempio \
    "https://github.com/home-assistant/tempio/releases/download/${TEMPIO_VERSION}/tempio_${BUILD_ARCH}"

# Copy root filesystem
COPY rootfs /

RUN apt-get update \
    && apt-get install -y fontconfig fonts-freefont-ttf \
    && rm -rf /var/lib/apt/lists/*

COPY --from=escpos /usr/src/app/escpos2mqtt /usr/bin/escpos2mqtt
