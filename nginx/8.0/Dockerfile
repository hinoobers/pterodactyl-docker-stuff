FROM eclipse-temurin:8u312-b07-jdk-focal

RUN         apt update \
            && apt install -y software-properties-common \
            && add-apt-repository ppa:ondrej/php \
            && apt -y install --no-install-recommends git php8.0 php8.0-fpm php8.0-curl ca-certificates nginx \
            && apt clean
            
USER container
ENV  USER container
ENV HOME /home/container

WORKDIR /home/container

COPY        ./nginx/entrypoint.sh /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]
