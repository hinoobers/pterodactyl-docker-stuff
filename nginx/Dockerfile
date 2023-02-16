FROM openjdk:8-jdk-alpine

RUN         apt-get update \
            && apt-get -y install --no-install-recommends git php8 \
            && apt-get clean
            
USER container
ENV  USER container
ENV HOME /home/container

WORKDIR /home/container

COPY ./nginx/entrypoint.sh /entrypoint.sh

CMD ["/bin/bash", "/entrypoint.sh"]
