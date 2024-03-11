FROM ubuntu:latest

# Install SSH server and other dependencies
RUN apt-get update && \
    apt-get install -y openssh-server


RUN apt-get install -y curl



#Install helm
RUN curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
RUN chmod 700 get_helm.sh
RUN ./get_helm.sh


# Create a non-root user (you can customize username and password)
ARG USERNAME=myuser
ARG PASSWORD=rootroot
RUN useradd -m -s /bin/bash ${USERNAME} && \
    echo "${USERNAME}:${PASSWORD}" | chpasswd && \
    usermod -aG sudo ${USERNAME}


# Set up SSH access
RUN mkdir /var/run/sshd

# Allow SSH access to container
EXPOSE 22

# Set working directory
WORKDIR /app

# Start SSH server and keep container running
CMD ["/usr/sbin/sshd", "-D"]

#CMD ["bash", "-c", "while true; do sleep 3600; done"]