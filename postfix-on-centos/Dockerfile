FROM centos

# リポジトリが参照しているミラーサイトの変更
RUN sed -i 's/^mirrorlist=/#&/' /etc/yum.repos.d/CentOS-Linux-BaseOS.repo && \
    sed -i 's/^#baseurl=/baseurl=/' /etc/yum.repos.d/CentOS-Linux-BaseOS.repo && \
    sed -i 's|^baseurl=http://mirror.centos.org/|baseurl=http://vault.centos.org/|' /etc/yum.repos.d/CentOS-Linux-BaseOS.repo

RUN sed -i 's/^mirrorlist=/#&/' /etc/yum.repos.d/CentOS-Linux-AppStream.repo && \
    sed -i 's/^#baseurl=/baseurl=/' /etc/yum.repos.d/CentOS-Linux-AppStream.repo && \
    sed -i 's|^baseurl=http://mirror.centos.org/|baseurl=http://vault.centos.org/|' /etc/yum.repos.d/CentOS-Linux-AppStream.repo

RUN yum clean all && \
    rm -rf /var/cache/yum && \
    yum makecache

RUN yum update -y

RUN yum install -y postfix

# IPv6を無効にする設定を追加
RUN sed -i 's/inet_protocols = all/inet_protocols = ipv4/' /etc/postfix/main.cf

RUN yum install -y mailx

CMD ["sh", "-c", "postfix start && /bin/bash"]
