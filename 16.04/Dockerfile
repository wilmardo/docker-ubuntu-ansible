FROM ubuntu:16.04

LABEL maintainer="Wilmar den Ouden <info@wilmardenouden.nl>"

ENV container docker

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
