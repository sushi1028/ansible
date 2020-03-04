FROM ubuntu:18.04

RUN apt update && apt upgrade -y 

RUN apt install -y software-properties-common

RUN apt-add-repository -y ppa:ansible/ansible && \
    apt update && apt install -y ansible python3 nano sudo openssh-server

RUN apt install net-tools iputils-ping -y

RUN echo "root:Docker!" | chpasswd

RUN mkdir /var/run/sshd
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

WORKDIR /root/.ssh
COPY ./keystore/* ./ 

WORKDIR /etc/ansible

RUN echo "export ANSIBLE_HOST_KEY_CHECKING=False" > /root/.bashrc

RUN echo '[servers] \n\
server1 ansible_host=10.5.0.6 \n\
server2 ansible_host=10.5.0.7 \n\
server3 ansible_host=10.5.0.8 \n\
server4 ansible_host=10.5.0.9 \n\
server5 ansible_host=10.5.0.10 \n\
server6 ansible_host=10.5.0.11 \n\
[servers:vars] \n\
ansible_python_interpreter=/usr/bin/python3' >> hosts

WORKDIR /root

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
