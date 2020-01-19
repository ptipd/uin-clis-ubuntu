FROM ptipd/uin-base-ubuntu:1.1_18.04

ARG APP_BUILD

RUN printf "Build of ${APP_BUILD}, date: %s\n" `date -u +"%Y-%m-%dT%H:%M:%SZ"` >> /etc/BUILD && \
    #
    # install web server and php:
    apt-get -y update && \
    apt-get -y install --no-install-recommends cron \
        logrotate mysql-client ldap-client iputils-ping && \
    #
    # prepare custom apache settings:
    #
    # cleanup:
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /usr/share/doc/* /usr/share/man/* && \
    rm -f /var/log/*log var/log/apt/*log

COPY base/entpoint.sh /app

ENTRYPOINT /app
