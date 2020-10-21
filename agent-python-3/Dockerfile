FROM quay.io/openshift/origin-jenkins-agent-base:v4.0

ENV LANG en_US.utf8
ENV LC_ALL en_US.utf8

COPY contrib/bin/configure-agent /usr/local/bin/configure-agent

# CentOS repositories
RUN rm /etc/yum.repos.d/* && curl http://mirror.centos.org/centos-7/7/os/x86_64/RPM-GPG-KEY-CentOS-7 -o /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
COPY contrib/openshift/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo

# Install python
RUN INSTALL_PKGS="python3-pip" && \
    yum install -y --setopt=tsflags=nodocs --disableplugin=subscription-manager $INSTALL_PKGS && \
    rpm -V $INSTALL_PKGS && \
    yum clean all -y

RUN chown -R 1001:0 $HOME && \
    chmod -R g+rw $HOME

USER 1001
