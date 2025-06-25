FROM eclipse-temurin:21-jdk-jammy

USER root

# Install dependencies
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
    python3-pip \
    && rm -rf /var/lib/apt/lists/*

# Install Firefox and Geckodriver (Linux AMD64 version)
RUN add-apt-repository -y ppa:mozillateam/ppa && \
    apt-get update && \
    apt-get install -y firefox-esr && \
    wget https://github.com/mozilla/geckodriver/releases/download/v0.33.0/geckodriver-v0.33.0-linux64.tar.gz && \
    tar -xzf geckodriver-v0.33.0-linux64.tar.gz && \
    mv geckodriver /usr/bin/geckodriver && \
    chmod +x /usr/bin/geckodriver && \
    rm geckodriver-v0.33.0-linux64.tar.gz && \
    rm -rf /var/lib/apt/lists/*

# Clone and build libllmodel.so from GPT4All
WORKDIR /opt

RUN git clone https://github.com/nomic-ai/gpt4all.git

WORKDIR /opt/gpt4all

RUN mkdir build

WORKDIR /opt/gpt4all/build

RUN cmake .. -DBUILD_SHARED_LIBS=ON -DCMAKE_BUILD_TYPE=Release -G Ninja && \
    ninja && \
    mkdir -p /usr/local/lib/llmodel && \
    cp libllmodel.so /usr/local/lib/llmodel/ && \
    echo "/usr/local/lib/llmodel" > /etc/ld.so.conf.d/llmodel.conf && \
    ldconfig

# Cleanup
WORKDIR /opt
RUN rm -rf gpt4all

# Switch back to container user
USER container
ENV USER container
ENV HOME /home/container

# Set working dir
WORKDIR /home/container

# Copy startup script
COPY ./java/entrypoint.sh /entrypoint.sh
CMD [ "/bin/bash", "/entrypoint.sh" ]
