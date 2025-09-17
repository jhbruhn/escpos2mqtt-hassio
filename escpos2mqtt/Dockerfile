ARG BUILD_FROM

FROM $BUILD_FROM AS build

RUN apk add --no-cache git rust cargo


WORKDIR /app
RUN git clone https://github.com/jhbruhn/escpos2mqtt.git

RUN cd escpos2mqtt && git checkout main &&cargo build --release

# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
FROM $BUILD_FROM

# Execute during the build of the image
ARG TEMPIO_VERSION BUILD_ARCH
RUN \
    curl -sSLf -o /usr/bin/tempio \
    "https://github.com/home-assistant/tempio/releases/download/${TEMPIO_VERSION}/tempio_${BUILD_ARCH}"

# Copy root filesystem
COPY rootfs /

COPY --from=build /app/escpos2mqtt/target/release/escpos2mqtt /usr/bin/escpos2mqtt
