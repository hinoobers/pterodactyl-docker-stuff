FROM        --platform=$TARGETOS/$TARGETARCH eclipse-temurin:19-jdk-jammy

RUN         apt-get update -y \
            && apt-get install -y lsof curl ca-certificates openssl git tar sqlite3 fontconfig libfreetype6 tzdata iproute2 libstdc++6 \
            && useradd -d /home/container -m container
            
RUN apt-get install -y wget
RUN wget -q https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
RUN apt-get install -y ./google-chrome-stable_current_amd64.deb

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        ./java/entrypoint.sh /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]
