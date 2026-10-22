FROM debian:11
# Debian 11 is end of life: its packages and security updates moved to archive.debian.org
RUN \
    for f in /etc/apt/sources.list /etc/apt/sources.list.d/*; do \
        [ -f "$f" ] && sed -i \
            -e 's|deb.debian.org/debian-security|archive.debian.org/debian-security|g' \
            -e 's|security.debian.org/debian-security|archive.debian.org/debian-security|g' \
            -e 's|deb.debian.org/debian|archive.debian.org/debian|g' \
            -e '/bullseye-updates/d' \
            "$f"; \
    done; \
    echo 'Acquire::Check-Valid-Until "false";' > /etc/apt/apt.conf.d/99archive && \
    dpkg --add-architecture i386 && \
    apt-get update && \
    apt-get install -y \
        ca-certificates \
        gpg \
        wget \
    && \
    apt-get install -y \
        ninja-build \
        clang-11 \
        python3-pip \
        gcc-10-multilib \
        g++-10-multilib \
        libstdc++-10-dev:i386 \
        libstdc++6:i386 \
        libc6:i386 \
    && \
    wget https://cmake.org/files/v3.20/cmake-3.20.6-linux-x86_64.tar.gz && \
    tar zxvf cmake-3.20.6-linux-x86_64.tar.gz && \
    mv cmake-3.20.6-linux-x86_64       /opt/cmake-3.20.6 && \
    ln -sf  /opt/cmake-3.20.6/bin/*    /usr/bin/ && \
    useradd -m user && \
    su user -c 'pip3 install --user conan'

USER user

ENV CC=/usr/bin/clang-11 \
    CXX=/usr/bin/clang++-11 \
    PATH=~/.local/bin:${PATH}

COPY docker-entrypoint.sh /
CMD /docker-entrypoint.sh
