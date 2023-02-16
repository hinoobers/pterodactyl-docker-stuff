FROM openjdk:8-jdk-alpine

RUN         apt update \
            && apt install git php8 \
            && apt clean
            
USER container
ENV  USER container
ENV HOME /home/container

WORKDIR /home/container

COPY ./nginx/entrypoint.sh /entrypoint.sh

CMD ["/bin/bash", "/entrypoint.sh"]
