FROM ubuntu:16.04

ENV container docker
ENV DEBIAN_FRONTEND noninteractive

LABEL maintainer="Wilmar den Ouden <info@wilmardenoude.nl>"

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        systemd \
        systemd-sysv \
        ca-certificates
    && apt-get clean

# We never want these to run in a container
RUN systemctl mask \
    dev-hugepages.mount \
    sys-fs-fuse-connections.mount \
    sys-kernel-config.mount \
    display-manager.service \
    getty@.service \
    systemd-logind.service \
    systemd-remount-fs.service \
    getty.target \
    graphical.target \
    kmod-static-nodes.service

RUN systemctl set-default multi-user.target

STOPSIGNAL SIGRTMIN+3

ENTRYPOINT ["/sbin/init"]
