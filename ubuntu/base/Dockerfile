FROM ubuntu:latest

# replace apt source
RUN cp /etc/apt/sources.list /etc/apt/sources.list.bak
COPY source.list /etc/apt/sources.list

# install ssh wget curl vim tar unzip
RUN apt-get update; apt-get upgrade -y && \
    apt-get install --no-install-recommends --no-install-suggests -y \
        openssh-server\
        wget curl vim tar unzip && \
    sed -i 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config && \
    echo "telnet stream tcp nowait telnetd /usr/sbin/tcpd /usr/sbin/in.telnetd" >> /etc/inetd.conf && \
    echo "root:root" | chpasswd && \
    useradd admin && \
    echo "admin:admin" | chpasswd && \
    echo "admin ALL=(ALL) ALL" >> /etc/sudoers  && \
    mkdir /home/admin && \
    mkdir /var/run/sshd && \
    # clear
    rm -rf /var/lib/apt/lists/*

EXPOSE 22
ENTRYPOINT /usr/sbin/sshd -D