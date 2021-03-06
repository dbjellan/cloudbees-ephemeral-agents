FROM node:current-alpine
LABEL maintainer "Your Name <first.last@merrillcorp.com>"

# install cURL, git, netbase, wget, and certificates
RUN apk update && apk add \
    ca-certificates \
    curl \
    netbase \
    wget \
    git \
    && rm -rf /var/lib/apt/lists/*

# install the CF CLI
RUN $ curl -L "https://cli.run.pivotal.io/stable?release=macosx64-binary&source=github" | tar -zx \
    && mv cf /usr/local/bin

# adding gnupg2 and dirmngr to handle gpg keys
RUN apk update && apk add \
    gnupg2 \
    dirmngr \
    && rm -rf /var/lib/apt/lists/*

# Installing the Jfrog CLI
RUN curl -fL https://getcli.jfrog.io | sh \
    && mv ./jfrog /usr/local/bin/jfrog \
    && chmod 776 /usr/local/bin/jfrog

# Installing Chrome headless
RUN echo @edge http://nl.alpinelinux.org/alpine/edge/community >> /etc/apk/repositories \
    && echo @edge http://nl.alpinelinux.org/alpine/edge/main >> /etc/apk/repositories \
    && apk add --no-cache \
    chromium@edge \
    harfbuzz@edge \
    nss@edge \
    && rm -rf /var/cache/* \
    && mkdir /var/cache/apk

# add Chrome env variables
ENV CHROME_BIN=/usr/bin/chromium-browser \
CHROME_PATH=/usr/lib/chromium/

ENTRYPOINT [ "node" ]
