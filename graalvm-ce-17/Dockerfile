# Use Bitnami Minideb as base image
FROM        bitnami/minideb:bookworm

# Set optional labels
LABEL       author="Blank517" maintainer="Blank517"

# Install required packages
RUN         install_packages ca-certificates curl locales jq iproute2

# Generate locale
RUN         echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && \
            locale-gen

ENV         LC_ALL=en_US.UTF-8 \
            LANG=en_US.UTF-8 \
            LANGUAGE=en_US.UTF-8

# Setup GraalVM 17 CE build
WORKDIR     /opt/

RUN         curl -JOLSs --retry 2 https://github.com/graalvm/graalvm-ce-builds/releases/download/jdk-17.0.9/graalvm-community-jdk-17.0.9_linux-aarch64_bin.tar.gz && \
            tar xzf graalvm-community-jdk-17.0.9_linux-aarch64_bin.tar.gz && \
            rm graalvm-community-jdk-17.0.9_linux-aarch64_bin.tar.gz

ENV         JAVA_HOME="/opt/graalvm-community-openjdk-17.0.9+9.1" \
            PATH="/opt/graalvm-community-openjdk-17.0.9+9.1/bin:$PATH"

# Pterodactyl related commands
RUN         adduser --home /home/container --disabled-password container

USER        container

ENV         USER=container HOME=/home/container

WORKDIR     /home/container

COPY        ./../entrypoint.sh /entrypoint.sh

CMD         ["/bin/bash", "/entrypoint.sh"]
