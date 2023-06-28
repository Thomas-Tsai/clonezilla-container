FROM tlinux/drbl:latest
MAINTAINER thomas _at_ clonezilla.org

VOLUME ["/tftpboot", "/home/", "/opt", "/usr", "/var"]
COPY drblpush.conf /etc/drbl/drblpush.conf
RUN sh -c 'echo "" |drblpush -c /etc/drbl/drblpush.conf'
ENTRYPOINT ["/autopush"]
