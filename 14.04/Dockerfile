FROM ubuntu:14.04

LABEL maintainer="Wilmar den Ouden <info@wilmardenouden.nl>"

ENV container docker

ADD init-fake.conf /etc/init/fake-container-events.conf

RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y \
            python \
            sudo \
            bash \
            ca-certificates \
    && apt-get clean


# undo some leet hax of the base image
RUN rm /usr/sbin/policy-rc.d; \
	rm /sbin/initctl; dpkg-divert --rename --remove /sbin/initctl

# remove some pointless services
RUN /usr/sbin/update-rc.d -f ondemand remove; \
	for f in \
		/etc/init/u*.conf \
		/etc/init/mounted-dev.conf \
		/etc/init/mounted-proc.conf \
		/etc/init/mounted-run.conf \
		/etc/init/mounted-tmp.conf \
		/etc/init/mounted-var.conf \
		/etc/init/hostname.conf \
		/etc/init/networking.conf \
		/etc/init/tty*.conf \
		/etc/init/plymouth*.conf \
		/etc/init/hwclock*.conf \
		/etc/init/module*.conf\
	; do \
		dpkg-divert --local --rename --add "$f"; \
	done;

STOPSIGNAL SIGRTMIN+3

ENTRYPOINT ["/sbin/init"]
