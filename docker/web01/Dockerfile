# Use the Ubuntu base image
FROM ubuntu

# Install necessary packages for SSH server
RUN apt-get update && apt-get install -y \
    openssh-server iputils-ping \
    && rm -rf /var/lib/apt/lists/*  # Clean up package lists

# Ensure SSH directory exists and set permissions
RUN mkdir -p /var/run/sshd && chmod 0755 /var/run/sshd

# Generate SSH host keys if not already generated
RUN test -f /etc/ssh/ssh_host_rsa_key || ssh-keygen -q -N '' -t rsa -f /etc/ssh/ssh_host_rsa_key
RUN test -f /etc/ssh/ssh_host_dsa_key || ssh-keygen -q -N '' -t dsa -f /etc/ssh/ssh_host_dsa_key
RUN test -f /etc/ssh/ssh_host_ecdsa_key || ssh-keygen -q -N '' -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key
RUN test -f /etc/ssh/ssh_host_ed25519_key || ssh-keygen -q -N '' -t ed25519 -f /etc/ssh/ssh_host_ed25519_key

# Configure SSH daemon
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config

# Expose SSH port
EXPOSE 22

# Start SSH daemon
CMD ["/usr/sbin/sshd", "-D"]
