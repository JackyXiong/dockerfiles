From ubuntu:14.04

MAINTAINER JackyXiong <xiongjiekobe@gmail.com>

# Base
RUN sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list && \
    apt-get update --fix-missing && apt-get -y upgrade
RUN apt-get install -y software-properties-common && \
    apt-get install -y byobu curl git vim wget unzip python-pip zsh
RUN apt-get install -y openssh-server && mkdir /var/run/sshd && \
    # 设置root用户和密码
    echo 'root:root' | chpasswd &&\
    # 允许root使用密码登录,详细可以man sshd_config
    sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed -i 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
RUN echo "export VISIBLE=now" >> /etc/profile &&\
    chsh -s /bin/zsh && cd ~; mkdir .ssh; echo > .ssh/authorized_keys
RUN sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
    # 安装 k-vim
RUN git clone https://github.com/wklken/vim-for-server.git && ln -s vim-for-server/vimrc ~/.vimrc

ENV NOTVISIBLE "in users profile"
EXPOSE 22 
EXPOSE 80
CMD ["/usr/sbin/sshd", "-D"]

