# Official base image
FROM kalilinux/kali-rolling

# Apt
RUN apt -yqq update && apt -yqq upgrade && apt -yqq autoremove && apt clean

RUN apt-get install hping3 fping slowhttptest siege -y && mkdir tools

WORKDIR /tools

COPY ./http-flood.sh /tools/
COPY ./icmp-flood.sh /tools/
COPY ./slowloris.sh /tools/
COPY ./syn-flood.sh /tools/
COPY ./udp-flood.sh /tools/
COPY ./set-backend.sh /tools/
COPY ./set-defender.sh /tools/
COPY ./ping-of-death.sh /tools/
COPY ./urls.txt /tools/
