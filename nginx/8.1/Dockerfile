FROM eclipse-temurin:8u312-b07-jdk-focal

RUN apt update \
    && apt install -y software-properties-common \
    && add-apt-repository ppa:ondrej/php \
    && apt -y install --no-install-recommends git curl php8.1 php8.1-fpm php8.1-curl ca-certificates nginx \
    && apt clean

# Install necessary PHP extensions
RUN apt -y install php8.1-mysql php8.1-mbstring php8.1-xml

USER container
ENV USER container
ENV HOME /home/container

WORKDIR /home/container

COPY ./nginx/entrypoint.sh /entrypoint.sh
CMD ["/bin/bash", "/entrypoint.sh"]
