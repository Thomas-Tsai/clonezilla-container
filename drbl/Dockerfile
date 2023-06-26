FROM debian:buster
MAINTAINER thomas _at_ clonezilla.org

RUN apt-get update
RUN apt-get -y install iproute2 net-tools vim gpg
RUN gpg --keyserver keyserver.ubuntu.com --recv 45599AFD
RUN gpg --export 667857D045599AFD |gpg --dearmour -o /etc/apt/trusted.gpg.d/drbl.gpg
RUN apt-get update
RUN apt-get install -y drbl
