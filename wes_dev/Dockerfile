ARG BUILD_FROM
FROM $BUILD_FROM

ARG TEMPIO_VERSION BUILD_ARCH
ARG WES2MQTT_VERSION=0.9.2-beta

RUN \
    curl -sSLf -o /usr/bin/tempio \
    "https://github.com/home-assistant/tempio/releases/download/${TEMPIO_VERSION}/tempio_${BUILD_ARCH}"

# Copy root filesystem
COPY rootfs /

RUN apk update 
RUN apk add openjdk21-jre

RUN curl -o /wes2mqtt.jar https://repo1.maven.org/maven2/org/rockhopper/smarthome/wes2mqtt/${WES2MQTT_VERSION}/wes2mqtt-${WES2MQTT_VERSION}.jar
