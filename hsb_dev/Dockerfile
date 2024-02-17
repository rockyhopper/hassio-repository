ARG BUILD_FROM
FROM $BUILD_FROM

ARG TEMPIO_VERSION BUILD_ARCH
ARG hsb2mqtt_version=dev-latest-SNAPSHOT

RUN \
    curl -sSLf -o /usr/bin/tempio \
    "https://github.com/home-assistant/tempio/releases/download/${TEMPIO_VERSION}/tempio_${BUILD_ARCH}"

# Copy root filesystem
COPY rootfs /

RUN apk update 
RUN apk add openjdk17

RUN echo "export HSB2MQTT_VERSION='$(curl https://s01.oss.sonatype.org/content/repositories/snapshots/org/rockhopper/smarthome/hsb2mqtt/${hsb2mqtt_version}/maven-metadata.xml \
| grep '<value>.*</value>' \
| tr -s " " \
| cut -d ">" -f2 \
| cut -d "<" -f1 \
| sort -V -r \
| head -1)'" >> /envfile

RUN . /envfile; curl -o /hsb2mqtt.jar https://s01.oss.sonatype.org/content/repositories/snapshots/org/rockhopper/smarthome/hsb2mqtt/dev-latest-SNAPSHOT/hsb2mqtt-$WES2MQTT_VERSION.jar

