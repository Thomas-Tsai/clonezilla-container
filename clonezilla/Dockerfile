FROM tlinux/drblsrv:latest
MAINTAINER thomas _at_ clonezilla.org

COPY drblpush.conf /etc/drbl/drblpush.conf
#RUN drblpush -c /etc/drbl/drblpush.conf
#RUN sed -i '/^\/home/d' /etc/exports
#RUN sed -i '/^\/opt/d' /etc/exports
#RUN sed -i '/^\/usr/d' /etc/exports
#RUN sed -i '/^\/var/d' /etc/exports
#RUN rpcbind
#RUN service nfs-kernel-server restart
#RUN drbl-ocs -b -l en_US.UTF-8 -y0 -p true select_in_client
VOLUME ["/tftpboot", "/home/partimag"]
#EXPOSE 68/udp 111/udp 2049/tcp
#CMD ["drbl-all-service start"]
