FROM ptipd/uin-clis-ubuntu:1.1_18.04-sshd

ARG APP_BUILD

RUN printf "Build of ${APP_BUILD}, date: %s\n" `date -u +"%Y-%m-%dT%H:%M:%SZ"` >> /etc/BUILD && \
    #
    # install base cli tools:
    apt-get -y update && \
    DEBIAN_FRONTEND=noninteractive DEBCONF_NONINTERACTIVE_SEEN=true \
        apt-get -y install --no-install-recommends \
        php7.2 php7.2-intl php7.2-gd php7.2-curl php7.2-ldap php7.2-mysql php7.2-sqlite3 \
        links lynx sendemail mutt shelldap mysql-client ldap-client && \
    echo 'root:5004' | chpasswd && \
    sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd && \
    echo 'export VISIBLE=now' >> /etc/profile && \
    mkdir /var/run/sshd && \
    #
    # cleanup:
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /usr/share/doc/* /usr/share/man/* && \
    rm -f /var/log/*log var/log/apt/*log
