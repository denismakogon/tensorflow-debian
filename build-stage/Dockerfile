FROM debian:stretch-slim

ENV BUILD_PACKAGES="\
        build-essential \
        linux-headers-4.9 \
        cmake \
        tcl-dev \
        xz-utils \
        zlib1g-dev \
        curl"
ENV APT_PACKAGES="git ca-certificates openssl gcc"

ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN set -ex; \
    apt-get update -y; \
    apt-get upgrade -y; \
    apt-get install -y --no-install-recommends ${BUILD_PACKAGES}; \
    apt-get install -y --no-install-recommends ${APT_PACKAGES}; \
    curl -L "https://storage.googleapis.com/tensorflow/libtensorflow/libtensorflow-cpu-linux-x86_64-1.6.0.tar.gz" | tar -C /usr/local -xz; \
    ldconfig; \
    curl -L "https://dl.google.com/go/go1.10.1.linux-amd64.tar.gz"  | tar -C /usr/local -xz; \
    mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"; \
    go version; \
    curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh; \
    apt-get remove --purge --auto-remove -y ${BUILD_PACKAGES}; \
    apt-get clean; \
    apt-get autoclean; \
    apt-get autoremove; \
    rm -rf /tmp/* /var/tmp/*; \
    rm -rf /var/lib/apt/lists/*; \
    rm -f /var/cache/apt/archives/*.deb \
        /var/cache/apt/archives/partial/*.deb \
        /var/cache/apt/*.bin; \
    rm -rf /root/.[acpw]*
