FROM eclipse-temurin:21-jdk-jammy

USER root

# Base dependencies
RUN apt-get update && apt-get install -y \
        curl \
        lsof \
        ca-certificates \
        openssl \
        git \
        tar \
        sqlite3 \
        wget \
        fontconfig \
        tzdata \
        iproute2 \
        libfreetype6 \
        tini \
        unzip \
        libglib2.0-0 \
        libnss3 \
        software-properties-common \
        build-essential \
        cmake \
        ninja-build \
        python3 \
        python3-pip

# Install Firefox + Geckodriver
RUN add-apt-repository -y ppa:mozillateam/ppa && \
    apt-get update && \
    apt-get install -y firefox-esr && \
    wget https://github.com/mozilla/geckodriver/releases/download/v0.33.0/geckodriver-v0.33.0-linux-aarch64.tar.gz && \
    tar -xzf geckodriver-v0.33.0-linux-aarch64.tar.gz && \
    mv geckodriver /usr/bin/geckodriver && \
    chmod +x /usr/bin/geckodriver && \
    rm geckodriver-v0.33.0-linux-aarch64.tar.gz

# Build and install libllmodel.so
WORKDIR /opt
RUN git clone https://github.com/nomic-ai/gpt4all.git && \
    cd gpt4all && \
    mkdir build && cd build && \
    cmake .. -DBUILD_SHARED_LIBS=ON -DCMAKE_BUILD_TYPE=Release -G Ninja && \
    ninja && \
    mkdir -p /usr/local/lib/llmodel && \
    cp libllmodel.so /usr/local/lib/llmodel/ && \
    echo "/usr/local/lib/llmodel" > /etc/ld.so.conf.d/llmodel.conf && \
    ldconfig && \
    cd /opt && rm -rf gpt4all

# Clean up APT
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Runtime user
USER container
ENV USER container
ENV HOME /home/container

# Working directory and startup
WORKDIR /home/container
COPY ./java/entrypoint.sh /entrypoint.sh
CMD [ "/bin/bash", "/entrypoint.sh" ]
