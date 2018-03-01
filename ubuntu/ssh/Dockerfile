FROM ubuntu:latest

RUN apt-get update; apt-get upgrade -y && \
    apt-get install -y openssh-server openbsd-inetd telnetd && \
    sed -i 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config && \
    echo "telnet stream tcp nowait telnetd /usr/sbin/tcpd /usr/sbin/in.telnetd" >> /etc/inetd.conf && \
    echo "root:root" | chpasswd && \
    useradd admin && \
    echo "admin:admin" | chpasswd && \
    echo "admin ALL=(ALL) ALL" >> /etc/sudoers  && \
    mkdir /home/admin && \
    mkdir /var/run/sshd

EXPOSE 22 23
ENTRYPOINT service openbsd-inetd start && /usr/sbin/sshd -D