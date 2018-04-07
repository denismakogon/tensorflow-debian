FROM debian:stretch-slim

ENV APT_PACKAGES="curl ca-certificates openssl"

RUN set -ex; \
    apt-get update -y; \
    apt-get install -y --no-install-recommends ${APT_PACKAGES}; \
    curl -L "https://storage.googleapis.com/tensorflow/libtensorflow/libtensorflow-cpu-linux-x86_64-1.6.0.tar.gz" | tar -C /usr/local -xz; \
    ldconfig; \
    apt-get remove --purge --auto-remove -y curl; \
    apt-get clean; \
    apt-get autoclean; \
    apt-get autoremove; \
    rm -rf /tmp/* /var/tmp/*; \
    rm -rf /var/lib/apt/lists/*; \
    rm -f /var/cache/apt/archives/*.deb \
        /var/cache/apt/archives/partial/*.deb \
        /var/cache/apt/*.bin; \
    rm -rf /root/.[acpw]*
