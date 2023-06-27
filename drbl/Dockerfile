FROM debian:buster
MAINTAINER thomas _at_ clonezilla.org

VOLUME ["/tftpboot", "/home/", "/opt", "/usr", "/var"]
RUN apt-get update
RUN apt-get -y install iproute2 net-tools vim gpg cpio
RUN gpg --keyserver keyserver.ubuntu.com --recv 45599AFD
RUN gpg --export 667857D045599AFD |gpg --dearmour -o /etc/apt/trusted.gpg.d/drbl.gpg
RUN echo 'deb http://free.nchc.org.tw/drbl-core drbl stable' >> /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y drbl
RUN sh -c 'echo "" |drblsrv -c n -g n  -l en_US.UTF-8 -k 2 -i -o 2'
COPY drblpush.conf /etc/drbl/drblpush.conf
RUN sh -c 'echo "" |drblpush -c /etc/drbl/drblpush.conf'
#CMD ["drbl-all-service start"]
