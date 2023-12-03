FROM --platform=$TARGETOS/$TARGETARCH eclipse-temurin:21-jdk-jammy

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
        snap
RUN snap install firefox

RUN wget https://github.com/mozilla/geckodriver/releases/download/v0.33.0/geckodriver-v0.33.0-linux-aarch64.tar.gz && \
    tar -xzf geckodriver-v0.33.0-linux-aarch64.tar.gz && \
    mv geckodriver /usr/bin/geckodriver && \
    chmod +x /usr/bin/geckodriver && \
    rm geckodriver-v0.33.0-linux-aarch64.tar.gz

USER container
ENV  USER container
ENV HOME /home/container

WORKDIR /home/container

COPY ./java/entrypoint.sh /entrypoint.sh
CMD [ "/bin/bash", "/entrypoint.sh" ]
