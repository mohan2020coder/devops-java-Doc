# Use the CentOS 7 base image
FROM fedora

# Install necessary packages for SSH server
RUN yum -y install openssh-server iputils && \
    yum clean all

# Generate host keys and set permissions
RUN ssh-keygen -A && \
    mkdir /var/run/sshd && \
    chmod 0755 /var/run/sshd

# Configure SSH daemon
RUN sed -i 's/#PermitRootLogin yes/PermitRootLogin yes/' /etc/ssh/sshd_config

# Expose SSH port
EXPOSE 22

# Start SSH daemon
CMD ["/usr/sbin/sshd", "-D"]
