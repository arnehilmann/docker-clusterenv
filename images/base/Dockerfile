FROM centos

MAINTAINER arne.hilmann@gmail.com

# add local repo
ADD res/ /

# install epel repos
RUN yum install -y /repo-base/epel-*.rpm

# update to latest
RUN yum update -y

# install/configure sshd
RUN yum install -y openssh-server
RUN mkdir /var/run/sshd/
RUN sed -ri "s/^#PermitRootLogin yes/PermitRootLogin yes/g;s/^UsePAM yes/#UsePAM yes/g;s/^#UsePAM no/UsePAM no/g;" /etc/ssh/sshd_config
RUN service sshd start

# minimal bash configuration
RUN echo "source /etc/bashrc" | tee -a /.bashrc /root/.bash_profile

# install/configure ssh + keys
RUN yum install -y openssh-clients
RUN ssh-keygen -q -t rsa -f /root/.ssh/id_rsa -N ""
RUN cp /root/.ssh/id_rsa.pub /root/.ssh/authorized_keys
RUN sed -ri "s/^#[[:space:]]*StrictHostKeyChecking .*$/StrictHostKeyChecking no/g;" /etc/ssh/ssh_config

# install/configure sudo
RUN yum install -y sudo
RUN sed -ri '/^Defaults[[:space:]]*requiretty/s/^/#/' /etc/sudoers

# dnsmasq
RUN yum install -y dnsmasq bind-utils

# dev env stuff
RUN yum install -y python-twisted hostexpand python-netifaces PyYAML python-docopt python-simplejson

# removing temp files
RUN yum clean all
