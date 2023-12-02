FROM        --platform=$TARGETOS/$TARGETARCH eclipse-temurin:21-jdk-jammy

RUN         apt-get update -y \
            && apt-get install -y lsof curl ca-certificates openssl git tar sqlite3 fontconfig libfreetype6 tzdata iproute2 libstdc++6 \
            && useradd -d /home/container -m container
            
RUN apt-get install -y chromium-browser

RUN         useradd -m -d /home/container -s /bin/bash container
USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

STOPSIGNAL SIGINT

COPY        ./java/entrypoint.sh /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]