FROM        --platform=$TARGETOS/$TARGETARCH alpine:3.19

LABEL       author="Blank517" maintainer="Blank517"

RUN         apk add --update --no-cache ca-certificates=20230506-r0 curl=8.5.0-r0 git=2.43.0-r0 jq=1.7.1-r0 wget=1.21.4-r0

WORKDIR     /opt/

RUN         curl -JOLSs --retry 3 https://github.com/graalvm/graalvm-ce-builds/releases/download/jdk-17.0.9/graalvm-community-jdk-17.0.9_linux-aarch64_bin.tar.gz
RUN         tar xzf graalvm-community-jdk-17.0.9_linux-aarch64_bin.tar.gz
RUN         rm graalvm-community-jdk-17.0.9_linux-aarch64_bin.tar.gz

ENV         JAVA_HOME="/opt/graalvm-community-openjdk-17.0.9+9.1" \
            PATH="/opt/graalvm-community-openjdk-17.0.9+9.1/bin:$PATH"

RUN         adduser -d /home/container -m container

USER        container
ENV         USER=container HOME=/home/container

WORKDIR     /home/container

COPY        ./../entrypoint.sh /entrypoint.sh

CMD         ["/bin/bash", "/entrypoint.sh"]
