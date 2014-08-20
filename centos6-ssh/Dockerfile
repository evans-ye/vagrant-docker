# Bring up sshd
FROM centos:centos6
MAINTAINER Evans Ye <innovansye@gmail.com>

# ssh
RUN yum -y install openssh-server openssh-clients
RUN sed -i.bak s/UsePAM\ yes/UsePAM\ no/g /etc/ssh/sshd_config

# setup vagrant account
RUN useradd vagrant
RUN mkdir /home/vagrant/.ssh
RUN chmod 0700 /home/vagrant/.ssh
RUN touch /home/vagrant/.ssh/authorized_keys
RUN curl https://raw.githubusercontent.com/mitchellh/vagrant/master/keys/vagrant.pub >> /home/vagrant/.ssh/authorized_keys
RUN chmod 0600 /home/vagrant/.ssh/authorized_keys
RUN chown -R vagrant:vagrant /home/vagrant/.ssh
RUN passwd -d vagrant
RUN yum -y install sudo
RUN echo "vagrant ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# prepare execution script
RUN touch /sbin/my_init
RUN echo "#!/bin/bash" >> /sbin/my_init
RUN echo "service sshd start" >> /sbin/my_init
RUN echo "/bin/bash" >> /sbin/my_init
RUN chmod +x /sbin/my_init
