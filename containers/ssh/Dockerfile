FROM sickp/alpine-sshd:latest
LABEL maintainer="ADGSENPAI"
RUN apk add sudo
RUN adduser -D -h /home/user -s /bin/sh user && \
    ( echo "user:user" | chpasswd )

RUN echo '%wheel ALL=(ALL) ALL' > /etc/sudoers.d/wheel
RUN adduser user wheel
