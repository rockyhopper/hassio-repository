ARG BUILD_FROM
FROM $BUILD_FROM

ARG TEMPIO_VERSION BUILD_ARCH GITHUB_USERNAME GITHUB_PUBLIC_TOKEN
ARG wes2mqtt_version=dev-latest-SNAPSHOT

RUN \
    curl -sSLf -o /usr/bin/tempio \
    "https://github.com/home-assistant/tempio/releases/download/${TEMPIO_VERSION}/tempio_${BUILD_ARCH}"

# Copy root filesystem
COPY rootfs /

# add Azul's public key
RUN wget -P /etc/apk/keys/ https://cdn.azul.com/public_keys/alpine-signing@azul.com-5d5dc44c.rsa.pub
# add the Azul APK repository
RUN echo "https://repos.azul.com/zulu/alpine" | tee -a /etc/apk/repositories
# update the list of packages
RUN apk update
RUN apk add zulu8-jdk maven

RUN export GITHUB_USERNAME=$GITHUB_USERNAME & export GITHUB_PUBLIC_TOKEN=$GITHUB_PUBLIC_TOKEN

RUN mvn -s /root/.m2/settings.xml org.apache.maven.plugins:maven-dependency-plugin:3.5.0:copy -Dmdep.stripVersion=true -Dmdep.stripClassifier=true -Dartifact=org.rockhopper.smarthome:wes2mqtt:$wes2mqtt_version -DoutputDirectory=/  

RUN unset GITHUB_USERNAME & unset GITHUB_TOKEN

RUN apk del maven && rm /var/cache/apk/*


