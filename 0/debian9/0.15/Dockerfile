FROM marketplace.gcr.io/google/debian9
ENV NODEEXPORTER_VERSION 0.15.2

ENV C2D_RELEASE=${NODEEXPORTER_VERSION}

ENV NODEEXPORTER_URL="https://github.com/prometheus/node_exporter/releases/download/v$NODEEXPORTER_VERSION/node_exporter-$NODEEXPORTER_VERSION.linux-amd64.tar.gz"
ENV NODEEXPORTER_SHA256 1ce667467e442d1f7fbfa7de29a8ffc3a7a0c84d24d7c695cc88b29e0752df37

RUN set -x && \
    apt-get update && apt-get install -qq -y wget && \
    mkdir nodeexporter-files && cd nodeexporter-files && \
    wget -O nodeexporter.tar.gz "$NODEEXPORTER_URL" && \
    echo "$NODEEXPORTER_SHA256 nodeexporter.tar.gz" | sha256sum -c - && \
    tar xfvz nodeexporter.tar.gz --strip-components=1 && \
    mv node_exporter /bin/ && \
    mkdir -p /usr/share/doc/nodeexporter && \
    mv LICENSE /usr/share/doc/nodeexporter && \
    cd - && rm -r nodeexporter-files

EXPOSE      9100
USER        nobody
ENTRYPOINT  [ "/bin/node_exporter" ]

