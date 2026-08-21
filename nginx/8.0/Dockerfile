FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        software-properties-common \
        gpg-agent \
        ca-certificates \
        curl \
        wget \
        git \
        nginx \
    && add-apt-repository ppa:ondrej/php \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        php8.0 \
        php8.0-fpm \
        php8.0-curl \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

USER container

ENV USER=container
ENV HOME=/home/container

WORKDIR /home/container

COPY ./nginx/entrypoint.sh /entrypoint.sh

CMD ["/bin/bash", "/entrypoint.sh"]
