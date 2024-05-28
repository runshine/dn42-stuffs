FROM ubuntu:latest

RUN mkdir -p /tmp && chmod 777 /tmp && mkdir -p /var/cache/apt/archives/partial /var/tmp/ && \
    apt-get update && apt-get install -y apt-utils

RUN apt-get update && \
    apt-get install -y curl cron iptables wireguard-tools iproute2 mtr inetutils-ping dnsutils

RUN apt-get update && \
    apt-get install -y tcpdump iperf3

RUN apt-get install -y bird2

RUN mkdir -p /etc/bird/peers && mkdir -p /run/bird/ && \
    touch /etc/bird/roa_dn42.conf && touch /etc/bird/roa_dn42_v6.conf

COPY ./wg-reresolve-dns.sh /usr/local/bin/wg-reresolve-dns.sh

COPY ./crontab.txt /crontab.txt
RUN crontab < /crontab.txt

COPY ./enterpoint.sh /enterpoint.sh

CMD ["/enterpoint.sh"]

