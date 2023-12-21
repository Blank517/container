FROM        bitnami/minideb:bookworm

LABEL       author="Blank517" maintainer="Blank517"

RUN         install_packages ca-certificates curl jq

WORKDIR     /opt/

RUN         curl -JOLSs --retry 3 https://github.com/graalvm/graalvm-ce-builds/releases/download/jdk-17.0.9/graalvm-community-jdk-17.0.9_linux-aarch64_bin.tar.gz
RUN         tar xzf graalvm-community-jdk-17.0.9_linux-aarch64_bin.tar.gz
RUN         rm graalvm-community-jdk-17.0.9_linux-aarch64_bin.tar.gz

ENV         LC_ALL=en_US.UTF-8
ENV         LANG=en_US.UTF-8
ENV         LANGUAGE=en_US.UTF-8

ENV         JAVA_HOME="/opt/graalvm-community-openjdk-17.0.9+9.1" \
            PATH="/opt/graalvm-community-openjdk-17.0.9+9.1/bin:$PATH"

RUN         adduser -h /home/container -S -D container

USER        container
ENV         USER=container HOME=/home/container

WORKDIR     /home/container

COPY        ./../entrypoint.sh /entrypoint.sh

CMD         ["/bin/bash", "/entrypoint.sh"]
