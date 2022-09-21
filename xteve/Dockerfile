FROM ghcr.io/aperim/nvidia-cuda-ffmpeg:latest

RUN apt-get update && \
    apt-get -y --allow-change-held-packages full-upgrade && \
    apt-get -y install vlc curl unzip sudo

RUN mkdir -p /opt/xteve /etc/xteve/config && \
    curl -L "https://github.com/xteve-project/xTeVe-Downloads/blob/master/xteve_linux_amd64.zip?raw=true" -o /opt/xteve/xteve.zip && \
    cd /opt/xteve && \
    unzip /opt/xteve/xteve.zip && \
    mv ./xteve /usr/bin/ && \
    chmod 755 /usr/bin/xteve && \
    rm -rf /var/lib/apt/lists/* /opt/xteve && \
    addgroup --gid 1000 xteve && \
    adduser --home /etc/xteve \
        --shell /usr/sbin/nologin \
        --no-create-home \
        --uid 1000 \
        --gid 1000 \
        --gecos xteve,xteve,,,xteve \
        --disabled-password \
        --disabled-login \
        xteve

COPY ./xteve/rootfs /

RUN chown 1000:1000 /etc/xteve /usr/bin/xteve

ARG BUILD_DESCRIPTION="nvidia cuda ffmpeg xteve"
ARG BUILD_NAME="nvidia cuda ffmpeg xteve"
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

ENV UID=1000
ENV GID=1000

LABEL \
    maintainer="Troy Kelly <troy@troykelly.com>" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Troy Kelly" \
    org.opencontainers.image.authors="Troy Kelly <troy@troykelly.com>" \
    org.opencontainers.image.licenses="Apache-2.0" \
    org.opencontainers.image.url="https://troykelly.com" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}

ENTRYPOINT ["docker-xteve-entrypoint"]
CMD ["-config=/etc/xteve/config", "-port=8080"]
