FROM ptipd/uin-clis-ubuntu:1.1_18.04-cron

ARG APP_BUILD

RUN printf "Build of ${APP_BUILD}, date: %s\n" `date -u +"%Y-%m-%dT%H:%M:%SZ"` >> /etc/BUILD && \
    #
    # install base cli tools:
    apt-get -y update && \
    apt-get -y install --no-install-recommends software-properties-common && \
    add-apt-repository ppa:ondrej/php && \
    DEBIAN_FRONTEND=noninteractive DEBCONF_NONINTERACTIVE_SEEN=true \
        apt-get -y install --no-install-recommends \
        php7.3 php7.3-intl php7.3-gd php7.3-curl php7.3-ldap php7.3-mysql php7.3-sqlite3 && \
        mysql-client ldap-client && \
    #
    # cleanup:
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /usr/share/doc/* /usr/share/man/* && \
    rm -f /var/log/*log var/log/apt/*log
