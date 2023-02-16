FROM eclipse-temurin:8u312-b07-jdk-focal

RUN         apt update \
            && apt install -y software-properties-common \
            && add-apt-repository ppa:ondrej/php \
            && apt install -y git php8.1 curl ca-certificates nginx \
            && apt clean
            
USER container
ENV  USER container
ENV HOME /home/container

WORKDIR /home/container

COPY        ./nginx/entrypoint.sh /entrypoint.sh
CMD         [ "/bin/ash", "/entrypoint.sh" ]
