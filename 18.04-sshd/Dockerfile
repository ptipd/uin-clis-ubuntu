FROM ptipd/uin-base-ubuntu:1.1_18.04

ARG CFG_ID
ARG APP_BUILD

RUN printf "Build of ${APP_BUILD}, date: %s\n" `date -u +"%Y-%m-%dT%H:%M:%SZ"` >> /etc/BUILD && \
    #
    # install base cli tools:
    apt-get -y update && \
    apt-get -y install --no-install-recommends file openssh-server \
        telnet iputils-ping traceroute && \
        socat sdcv vim bash-completion bc lzop vifm tmux screen tree socket mc links curl source-highlight pv lynx vfu ytree wput lshw nmap bmon tshark sqlite3 \
shelldap mysql-client ldap-client 
dos2unix html2text sc csvtool jq ftp ncftp tftp sendemail multitail rar unrar mutt
    #
    # prepare config user:
    groupadd -g ${CFG_ID} cfg && \
    useradd -u ${CFG_ID} -g cfg -s /usr/sbin/nologin -d /opt cfg && \
    #
    # prepare entrypoint:
    echo '#!/bin/sh' > /app && \
    echo 'sshd' >> /app && \
    chmod +x /app && \
    #
    # cleanup:
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /usr/share/doc/* /usr/share/man/* && \
    rm -f /var/log/*log var/log/apt/*log

ENTRYPOINT /app
