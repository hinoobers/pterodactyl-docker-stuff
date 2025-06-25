FROM eclipse-temurin:21-jdk-jammy

USER root

RUN apt-get update && apt-get install -y \
        curl \
        lsof \
        ca-certificates \
        openssl \
        git \
        tar \
        sqlite3 \
        wget \
        fontconfig \
        tzdata \
        iproute2 \
        libfreetype6 \
        tini \
        unzip \
        libglib2.0-0 \
        libnss3 \
        software-properties-common # Added for add-apt-repository

RUN add-apt-repository -y ppa:mozillateam/ppa && \
    apt-get update && \
    apt-get install -y firefox-esr && \
    wget https://github.com/mozilla/geckodriver/releases/download/v0.33.0/geckodriver-v0.33.0-linux-aarch64.tar.gz && \
    tar -xzf geckodriver-v0.33.0-linux-aarch64.tar.gz && \
    mv geckodriver /usr/bin/geckodriver && \
    chmod +x /usr/bin/geckodriver && \
    rm geckodriver-v0.33.0-linux-aarch64.tar.gz && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

USER container
ENV USER container
ENV HOME /home/container

WORKDIR /home/container

COPY ./java/entrypoint.sh /entrypoint.sh
CMD [ "/bin/bash", "/entrypoint.sh" ]
