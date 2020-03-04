FROM ubuntu:18.04

RUN apt update && apt upgrade -y 

RUN apt install -y software-properties-common

RUN apt-add-repository -y ppa:ansible/ansible && \
    apt update && apt install -y python3 nano sudo openssh-server

RUN apt install net-tools -y
RUN echo "root:Docker!" | chpasswd

RUN mkdir /var/run/sshd
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

WORKDIR /root/.ssh
COPY ./authorized_keys . 

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]