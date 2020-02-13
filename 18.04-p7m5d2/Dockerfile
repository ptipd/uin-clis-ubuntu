FROM ptipd/uin-clis-ubuntu:1.4_18.04-cron3.0

ARG APP_BUILD

RUN printf "Build of ${APP_BUILD}, date: %s\n" `date -u +"%Y-%m-%dT%H:%M:%SZ"` >> /etc/BUILD && \
    #
    # install base cli tools:
    apt-get -y update && \
    apt-get -y install  && \
    DEBIAN_FRONTEND=noninteractive DEBCONF_NONINTERACTIVE_SEEN=true \
        apt-get -y install --no-install-recommends \
        php7.2 php7.2-intl php7.2-gd php7.2-curl php7.2-ldap php7.2-mysql php7.2-sqlite3 \
        mysql-client && \
    #
    # cleanup:
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /usr/share/doc/* /usr/share/man/* && \
    rm -f /var/log/*log var/log/apt/*log
