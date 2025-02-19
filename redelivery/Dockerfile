# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
ARG BUILD_FROM
FROM $BUILD_FROM

ARG TEMPIO_VERSION BUILD_ARCH
RUN \
    curl -sSLf -o /usr/bin/tempio \
    "https://github.com/home-assistant/tempio/releases/download/${TEMPIO_VERSION}/tempio_${BUILD_ARCH}"

# Download latest redelivery-core binary
RUN \
    curl -L -s \
        "https://github.com/proconlon/redelivery-core/releases/latest/download/redelivery-core-${BUILD_ARCH}" \
        -o /usr/bin/redelivery-core \
    && chmod a+x /usr/bin/redelivery-core

# Copy root file system (with S6 service files)
COPY rootfs/ /
RUN chmod a+x /etc/services.d/redelivery/run

EXPOSE 8080
