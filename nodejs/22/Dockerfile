FROM        node:22-bullseye-slim

RUN         apt-get update \
            && apt-get -y install --no-install-recommends curl ffmpeg iproute2 git sqlite3 python3 python3-pip python3-venv tzdata ca-certificates dnsutils build-essential locales default-jre \
            && pip3 install --no-cache-dir yt-dlp \
            && npm -g install npm@latest \
            && apt-get clean \
            && rm -rf /var/lib/apt/lists/* \
            && useradd -m -d /home/container container \
            && locale-gen en_US.UTF-8

RUN         npm install typescript ts-node @types/node --location=global   

ENV         LC_ALL=en_US.UTF-8
ENV         LANG=en_US.UTF-8
ENV         LANGUAGE=en_US.UTF-8

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        ./nodejs/entrypoint.sh /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]
