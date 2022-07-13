FROM node:current-alpine as builder
RUN apk add -U build-base python3
WORKDIR /usr/src/app
COPY . /usr/src/app
RUN yarn && \
    yarn build && \
    yarn install --production --ignore-scripts --prefer-offline

FROM node:current-alpine
LABEL maintainer="ADGSENPAI"
WORKDIR /usr/src/app
ENV NODE_ENV=production
EXPOSE 3000

RUN apk update
RUN apk add make automake gcc g++ subversion python3-dev

RUN apk add sudo
RUN adduser -D -h /home/adgsenpai -s /bin/sh adgsenpai && \
    ( echo "adgsenpai:test" | chpasswd )

RUN adduser -D -h /home/user -s /bin/sh user && \
    ( echo "user:user" | chpasswd )

RUN echo '%wheel ALL=(ALL) ALL' > /etc/sudoers.d/wheel
RUN adduser adgsenpai wheel
RUN adduser user wheel





RUN apk add python3
RUN apk add py3-pip
RUN apk add bash
RUN apk add curl
RUN apk add openssh
RUN printf '[ -z "$SSH_CLIENT" ] && source <(curl --fail --retry 3 -sSL "$HEROKU_EXEC_URL")' > /etc/profile.d/heroku-exec.sh

RUN printf 'WELCOME TO THE ADGSTUDIOS WEBOS LAB\nWE HOPE YOU HAVE FUN!\n' > /etc/motd

RUN rm /bin/sh && ln -s /bin/bash /bin/sh

COPY --from=builder /usr/src/app/build /usr/src/app/build
COPY --from=builder /usr/src/app/node_modules /usr/src/app/node_modules
COPY package.json /usr/src/app
RUN apk add -U coreutils openssh-client sshpass && \
    mkdir ~/.ssh

ENTRYPOINT ["yarn", "start"]
