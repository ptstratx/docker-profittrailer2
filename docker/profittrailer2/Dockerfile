FROM openjdk:8-jre-alpine

LABEL maintainer="https://github.com/ptstratx"

RUN apk add --no-cache curl \
    unzip \
    jq

RUN mkdir -p /opt && \
    URL=$(curl -s https://api.github.com/repos/taniman/profit-trailer/releases | jq -r '.[0].assets[0].browser_download_url') && \
    curl -Ls "$URL" > /opt/profittrailer.zip && \
    unzip -q /opt/profittrailer.zip -d /opt && \
    rm /opt/profittrailer.zip

EXPOSE 8081

ENV SPRING_PROFILES_ACTIVE production
# Their defaults
ENV SERVER_PORT 8081
ENV SERVER_TEST_MODE false
ENV SERVER_SITENAME ProfitTrailer2
ENV TRADING.LOG_HISTORY 8
ENV SERVER_DISABLE_PASSWORD false
ENV SERVER_TIMEZONE_OFFSET +00:00
ENV SERVER_LANGUAGE engb
ENV SERVER_SKIN dark
ENV SERVER_CURRENCY USD
ENV SERVER_DISABLE_NOTIFICATION true
ENV SERVER_DISABLE_BROWSER false
ENV SERVER_ENABLE_SHUTDOWN true
ENV SERVER_DISBALE_CONFIG false
ENV SERVER_DISABLE_ONLINE_CONFIG false
ENV SERVER_START_TRADING_DELAY 0
ENV TELEGRAM_DISABLE_NOTIFICATION false
ENV TELEGRAM_STARTUP_NOTIFICATION true
ENV DISCORD_STARTUP_NOTIFICATION true
ENV TELEGRAM_SHUTDOWN_NOTIFICATION true
ENV DISCORD_SHUTDOWN_NOTIFICATION true
ENV CONNECTION_TIMEOUT 30
ENV LOGGING_LEVEL_NL_KOMTEK info
WORKDIR /opt/ProfitTrailer/

COPY application.template /opt/ProfitTrailer/
COPY docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["java", "-jar", "ProfitTrailer.jar", "-XX:+UseConcMarkSweepGC", "-Xmx512m", "-Xms512m"]
