FROM eclipse-temurin:8u312-b07-jdk-focal

RUN         apt update \
            && apt install git php8.1 \
            && apt clean
            
USER container
ENV  USER container
ENV HOME /home/container

WORKDIR /home/container

COPY ./nginx/entrypoint.sh /entrypoint.sh

CMD ["/bin/bash", "/entrypoint.sh"]
