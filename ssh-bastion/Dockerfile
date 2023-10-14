FROM centos

# リポジトリが参照しているミラーサイトの変更
RUN sed -i 's/^mirrorlist=/#&/' /etc/yum.repos.d/CentOS-Linux-BaseOS.repo && \
    sed -i 's/^#baseurl=/baseurl=/' /etc/yum.repos.d/CentOS-Linux-BaseOS.repo && \
    sed -i 's|^baseurl=http://mirror.centos.org/|baseurl=http://vault.centos.org/|' /etc/yum.repos.d/CentOS-Linux-BaseOS.repo

RUN sed -i 's/^mirrorlist=/#&/' /etc/yum.repos.d/CentOS-Linux-AppStream.repo && \
    sed -i 's/^#baseurl=/baseurl=/' /etc/yum.repos.d/CentOS-Linux-AppStream.repo && \
    sed -i 's|^baseurl=http://mirror.centos.org/|baseurl=http://vault.centos.org/|' /etc/yum.repos.d/CentOS-Linux-AppStream.repo

# Install SSH Server
RUN yum -y update && yum -y install openssh-server openssh-clients

# Setup SSH Server
RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
RUN ssh-keygen -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key
RUN ssh-keygen -t ed25519 -f /etc/ssh/ssh_host_ed25519_key

# Root password
RUN echo "root:root" | chpasswd

# Run SSHD
CMD ["/usr/sbin/sshd", "-D"]
