FROM debian:stretch-slim

LABEL maintainer="https://github.com/ptstratx"

#RUN apk add --no-cache curl \
#    unzip \
#    jq

RUN apt-get update && apt-get install -y curl unzip jq && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /opt && \
    URL=$(curl -s https://api.github.com/repos/bTayFla/PtTracker/releases | jq -r '.[0].assets[1].browser_download_url') && \
    curl -Ls "$URL" > /opt/pttracker.zip && \
    unzip -q /opt/pttracker.zip -d /opt && \
    rm /opt/pttracker.zip

EXPOSE 3000

ENV SERVER_SITENAME ProfitTrailer2
ENV SERVER_CURRENCY USD

WORKDIR /opt/PtTracker/

COPY PtTracker.template /opt/PtTracker/
COPY docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["./PtTracker"]
