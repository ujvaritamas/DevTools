#FROM jenkins/agent
#USER root
#RUN apt update && curl -fsSL https://get.docker.com | sh
#RUN usermod -aG docker jenkins
#USER jenkins

FROM ubuntu:latest

RUN apt-get update \
    && apt-get install -y openssh-server \
    && mkdir /var/run/sshd \
    && useradd -rm -d /home/jenkins -s /bin/bash -g root -G sudo jenkins \
    && echo 'jenkins:rootroot' | chpasswd \
    && apt-get install -y openjdk-17-jre \
    && apt-get install -y openjdk-17-jdk

ENV JAVA_HOME=/usr/local/java
ENV PATH=${PATH}:${JAVA_HOME}/bin
RUN java -version

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]