FROM debian:stable-slim as setup
RUN DEBIAN_FRONTEND=noninteractive \
    apt-get update \
    && apt-get install -y gcc autoconf make automake libtool

# Statically linked binaries
FROM setup as build
WORKDIR /opt/libmspack
ADD . .
RUN ./cleanup.sh \
    && ./autogen.sh \
    && ./configure LDFLAGS=-static \
    && make

# # Dynamically linked binaries
# FROM setup as build
# WORKDIR /opt/libmspack
# ADD . .
# RUN ./rebuild.sh && make