FROM        --platform=$TARGETOS/$TARGETARCH eclipse-temurin:21-jdk-jammy

RUN         apt update -y \
            && apt install -y \
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
                tini
            
RUN  add-apt-repository ppa:savoury1/ffmpeg4
RUN  add-apt-repository ppa:savoury1/chromium
RUN  apt-get update -y
RUN  apt-get install -y chromium-browser

USER container
ENV  USER container
ENV HOME /home/container

WORKDIR /home/container

COPY        ./java/entrypoint.sh /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]
