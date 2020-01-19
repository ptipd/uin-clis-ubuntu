FROM ptipd/uin-base-ubuntu:1.1_18.04

ARG CFG_ID
ARG APP_BUILD

RUN printf "Build of ${APP_BUILD}, date: %s\n" `date -u +"%Y-%m-%dT%H:%M:%SZ"` >> /etc/BUILD && \
    #
    # install base cli tools:
    apt-get -y update && \
    apt-get -y install --no-install-recommends cron \
        logrotate iputils-ping && \
    #
    # prepare config user:
    groupadd -g ${CFG_ID} cfg && \
    useradd -u ${CFG_ID} -g cfg -s /usr/sbin/nologin -d /opt cfg && \
    #
    # prepare entrypoint:
    echo '#!/bin/sh' > /app && \
    echo 'cron -f' >> /app && \
    #
    # cleanup:
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /usr/share/doc/* /usr/share/man/* && \
    rm -f /var/log/*log var/log/apt/*log

ENTRYPOINT /app
