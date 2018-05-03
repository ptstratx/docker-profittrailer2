FROM openjdk:8-jre-alpine

LABEL maintainer="https://github.com/ptstratx"

RUN apk add --no-cache curl \
    unzip \
    jq

RUN mkdir -p /opt && \
    mkdir -p /opt/ptnotifications/ && \
    URL=$(curl -s https://api.github.com/repos/Roy4lz/ptnotifications/releases | jq -r '.[0].assets[0].browser_download_url') && \
    curl -Ls "$URL" > /opt/ptnotifications.zip && \
    unzip -q /opt/ptnotifications.zip -d /opt/ptnotifications/ && \
    rm /opt/ptnotifications.zip


ENV SPRING_PROFILES_ACTIVE production
# Their defaults
ENV PROFITTRAILER_INSTANCES 1
ENV TELEGRAM_ENABLED FALSE
ENV DISCORD_ENABLED FALSE
ENV SELL_NOTIFICATION TRUE
ENV BUY_NOTIFICATION TRUE
ENV SOM_NOTIFICATION TRUE
ENV ERROR_NOTIFICATION TRUE
ENV UPDATE_NOTIFICATION TRUE
ENV ENABLE_SETTINGS TRUE

WORKDIR /opt/ptnotifications

COPY settings.template /opt/ptnotifications
COPY docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["java", "-jar", "PTNotifications.jar", "-XX:+UseConcMarkSweepGC", "-Xmx64m", "-Xms64m"]
