FROM ghcr.io/jhbruhn/escpos2mqtt:main as escpos2mqtt

ARG BUILD_FROM

# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
FROM $BUILD_FROM

# Execute during the build of the image
ARG TEMPIO_VERSION BUILD_ARCH
RUN \
    curl -sSLf -o /usr/bin/tempio \
    "https://github.com/home-assistant/tempio/releases/download/${TEMPIO_VERSION}/tempio_${BUILD_ARCH}"

# Copy root filesystem
COPY rootfs /

COPY --from=escpos2mqtt /usr/src/app/escpos2mqtt /usr/bin/escpos2mqtt
