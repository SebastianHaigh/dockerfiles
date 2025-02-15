FROM debian:latest

# Install dependencies required to build Git
RUN apt update && apt install -y \
    gcc g++ make autoconf curl gettext \
    libcurl4-openssl-dev libexpat1-dev zlib1g-dev \
    libssl-dev tcl tk perl \
    python3 python3-pip \
    asciidoc xmlto docbook2x \
    less \
    && apt clean

