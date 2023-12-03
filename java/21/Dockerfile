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
        libglib2.0-0 \
        libnss3 \
        firefox

USER container
ENV  USER container
ENV HOME /home/container

WORKDIR /home/container

COPY ./java/entrypoint.sh /entrypoint.sh
CMD [ "/bin/bash", "/entrypoint.sh" ]
