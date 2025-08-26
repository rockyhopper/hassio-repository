ARG BUILD_FROM
FROM $BUILD_FROM

ARG TEMPIO_VERSION BUILD_ARCH
ARG hsb_version=0.9.1-beta

RUN \
    curl -sSLf -o /usr/bin/tempio \
    "https://github.com/home-assistant/tempio/releases/download/${TEMPIO_VERSION}/tempio_${BUILD_ARCH}"

# Copy root filesystem
COPY rootfs /

RUN apk update 
RUN apk add openjdk21

RUN echo "export HSB_VERSION='$(curl https://repo1.maven.org/maven2/org/rockhopper/smarthome/hsb/${hsb_version}/maven-metadata.xml \
| grep '<value>.*</value>' \
| tr -s " " \
| cut -d ">" -f2 \
| cut -d "<" -f1 \
| sort -V -r \
| head -1)'" >> /envfile

RUN . /envfile; curl -o /hsb.jar https://repo1.maven.org/maven2/org/rockhopper/smarthome/hsb/${hsb_version}/hsb-${HSB_VERSION}.jar

