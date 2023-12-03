FROM --platform=$TARGETOS/$TARGETARCH eclipse-temurin:21-jdk-jammy

RUN apt-get update && apt-get install -y \
        curl \
        lsof \
        ca-certificates \
        openssl \
        git \
        tar \
        sqlite3 \
        fontconfig \
        tzdata \
        iproute2 \
        libfreetype6 \
        tini \
        unzip \
        libglib2.0-0

# Download and install Chromedriver
RUN mkdir -p /tmp/chromedriver \
    && curl -SL https://github.com/electron/electron/releases/download/v27.1.3/chromedriver-v27.1.3-linux-arm64.zip -o /tmp/chromedriver/chromedriver.zip \
    && unzip -j /tmp/chromedriver/chromedriver.zip -d /tmp/chromedriver \
    && chmod +x /tmp/chromedriver/chromedriver \
    && mv /tmp/chromedriver/chromedriver /usr/bin/chromedriver \
    && rm -rf /tmp/chromedriver

USER container
ENV  USER container
ENV HOME /home/container

WORKDIR /home/container

COPY ./java/entrypoint.sh /entrypoint.sh
CMD [ "/bin/bash", "/entrypoint.sh" ]
