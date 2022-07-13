FROM sickp/alpine-sshd:latest
RUN adduser -D -h /home/adgsenpai -s /bin/sh term && \
    ( echo "adgsenpai:test" | chpasswd )

RUN adduser -D -h /home/user -s /bin/sh user && \
    ( echo "user:user" | chpasswd )