ARG OWN_BASE
FROM ${OWN_BASE}

ARG CFG_ID
ARG APP_BUILD

RUN printf "Build of ${APP_BUILD}, date: %s\n" `date -u +"%Y-%m-%dT%H:%M:%SZ"` >> /etc/BUILD && \
    #
    # install base cli tools:
    apt-get -y update && \
     DEBIAN_FRONTEND=noninteractive DEBCONF_NONINTERACTIVE_SEEN=true \
        apt-get -y install --no-install-recommends sudo openssh-server \
        nmap bmon ncftp tftp socat sc lzop pv ytree \
        bash-completion source-highlight rar unrar zip unzip \
        htop tmux screen vim mc vifm vfu && \
    #
    # prepare config user:
    groupadd -g ${CFG_ID} cfg && \
    useradd -u ${CFG_ID} -g cfg -s /usr/sbin/nologin -d /opt cfg && \
    #
    # prepare entrypoint:
    echo '#!/bin/sh' > /app && \
    echo '/usr/sbin/sshd -D' >> /app && \
    chmod 750 /app && \
    #
    # cleanup:
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /usr/share/doc/* /usr/share/man/* && \
    rm -f /var/log/*log var/log/apt/*log

EXPOSE 22

ENTRYPOINT /app
