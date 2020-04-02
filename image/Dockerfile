FROM centos:7

ENV container=docker SYSTEMD_LOG_TARGET=console

RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;

RUN \
    yum install -y openssh-server openssh-clients \
 && systemctl enable sshd \
 && yum install -y pacemaker pcs psmisc \
 && systemctl enable pcsd \
 && yum clean all

VOLUME /sys/fs/cgroup
VOLUME /persistent

CMD ["/lib/systemd/systemd"]
