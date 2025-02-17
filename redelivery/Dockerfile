# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
ARG BUILD_FROM
FROM $BUILD_FROM

WORKDIR /app

ARG TEMPIO_VERSION BUILD_ARCH
RUN \
    curl -sSLf -o /usr/bin/tempio \
    "https://github.com/home-assistant/tempio/releases/download/${TEMPIO_VERSION}/tempio_${BUILD_ARCH}"

# Copy the compiled Go binary from GitHub Actions or tasks.json output
COPY redelivery-${BUILD_ARCH} /app/redelivery
RUN chmod +x /app/redelivery

# Copy root file system (with S6 service files)
COPY rootfs/ /
RUN chmod +x /etc/services.d/redelivery/run

EXPOSE 3140

CMD [ "/etc/services.d/redelivery/run" ]