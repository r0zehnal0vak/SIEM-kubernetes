### Serves for building the image for Snort
# image: <dockerhub-username>:snort
# tag: 0.0.2 # current version, increase if changes occur

# docker build -t <dockerhub-username>/snort:<version> .
# docker push <dockerhub-username>/snort:<version>

# Use Ubuntu as the base image
FROM ubuntu:20.04

# Set environment variables to avoid interactive prompts
ENV DEBIAN_FRONTEND=noninteractive

# Install dependencies including iputils-ping
RUN apt-get update && apt-get install -y \
    build-essential \
    libpcap-dev \
    libpcre3-dev \
    iproute2 \
    libnet1-dev \
    zlib1g-dev \
    luajit \
    hwloc \
    libdumbnet-dev \
    liblzma-dev \
    openssl \
    libssl-dev \
    pkg-config \
    libhwloc-dev \
    cmake \
    libsqlite3-dev \
    uuid-dev \
    libcmocka-dev \
    libnetfilter-queue-dev \
    libmnl-dev \
    autotools-dev \
    libluajit-5.1-dev \
    libunwind-dev \
    libfl-dev \
    git \
    nano \
    wget \
    curl \
    ca-certificates \
    postgresql-client \
    snort \
    iputils-ping && \
    apt-get clean && rm -rf /var/lib/apt/lists/*  # Ensure proper line continuation

# Set up Snort directories
RUN mkdir -p /usr/local/etc/snort /var/log/snort /usr/local/lib/snort_dynamicrules

# Expose the necessary ports for Snort
EXPOSE 8080

# Default command to run Snort in daemon mode
CMD ["snort", "-c", "/usr/local/etc/snort/snort.lua", "-R", "/usr/local/etc/rules/local.rules", "-i", "eth0", "-D", "-l", "/var/log/snort"]
