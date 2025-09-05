FROM ubuntu:22.04

# Set environment variables to avoid interactive prompts
ENV DEBIAN_FRONTEND=noninteractive

# Update and install sudo
RUN apt-get update && \
    apt-get -y install sudo

# Install basic tools
RUN apt-get update && \
    apt-get install -y \
    curl \
    unzip \
    gnupg \
    software-properties-common \
    wget \
    git \
    lsb-release

# Install Azure CLI
RUN curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash

# Install Terraform using the new GPG key method
RUN wget -O- https://apt.releases.hashicorp.com/gpg | \
    gpg --dearmor | \
    sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
    https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
    sudo tee /etc/apt/sources.list.d/hashicorp.list && \
    apt-get update && \
    apt-get install terraform -y

# Install TFLint
RUN curl -s https://raw.githubusercontent.com/terraform-linters/tflint/master/install_linux.sh | bash

# Clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Reset environment variable
ENV DEBIAN_FRONTEND=dialog