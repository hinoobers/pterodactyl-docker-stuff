FROM eclipse-temurin:8u312-b07-jdk-focal

RUN         apt update \
            && apt install -y software-properties-common \
            && add-apt-repository ppa:ondrej/php \
            && apt -y install --no-install-recommends git php8.1 php8.1-fpm ca-certificates nginx \
            && apt clean
RUN apt -y install php8.1-mysql
            
USER container
ENV  USER container
ENV HOME /home/container

WORKDIR /home/container

COPY        ./nginx/entrypoint.sh /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]
