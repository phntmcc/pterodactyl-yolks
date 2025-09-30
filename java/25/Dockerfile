FROM --platform=$TARGETOS/$TARGETARCH eclipse-temurin:25-jdk

LABEL author="Robert Jansen" maintainer="rjansengd@gmail.com"
LABEL org.opencontainers.image.source="https://github.com/phntmcc/pterodactyl-yolks"
LABEL org.opencontainers.image.licenses="MIT"

# Optional: remove disk fillers many hosts block anyway
RUN rm -f /usr/bin/dd /usr/bin/fallocate /usr/bin/truncate /usr/bin/xfs_mkfile || true

# Base packages commonly used by MC servers on yolks
RUN apt-get update -y \
 && apt-get install -y --no-install-recommends \
    curl jq unzip lsof ca-certificates openssl git tar sqlite3 fontconfig libfreetype6 tzdata iproute2 libstdc++6 \
 && rm -rf /var/lib/apt/lists/*

# (Optional) MC AntiMalware
RUN curl -sSL https://github.com/OpticFusion1/MCAntiMalware/releases/latest/download/MCAntiMalware.jar -o /MCAntiMalware.jar

# Pterodactyl container user & home
RUN useradd -d /home/container -m container
USER container
ENV USER=container HOME=/home/container
WORKDIR /home/container

# Standard Pterodactyl entrypoint (lets Wings pass your Start Command)
COPY ./entrypoint.sh /entrypoint.sh
CMD ["/bin/bash", "/entrypoint.sh"]
