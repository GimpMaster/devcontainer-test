# Use Ubuntu 22.04 as the base image
FROM ubuntu:22.04

####################################################################################################
#
# Installation of Packages
#
# In this section we will install and setup all the tools needed for a standard backend devcontainer
#
####################################################################################################

# Update the package list and install essential tools
RUN apt-get update && apt-get install -y \
    curl \
    wget \
    gnupg \
    git \
    mariadb-client

# Add the Node.js 20 LTS repository
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash -

# Install Node.js and npm
RUN apt-get install -y nodejs

# Cleanup unnecessary packages and cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Verify Node.js and npm installation
RUN node -v
RUN npm -v

####################################################################################################
#
# Setup of dev user
#
# Here we make a non-root user with sudo access. Not sure if we should stick with root or not.
# I'm thinking we should be non-root for future where we start accessing the local user /dev
# folder to program android devices and such.
#
####################################################################################################


# This Dockerfile adds a non-root user with sudo access. Use the "remoteUser"
# property in devcontainer.json to use it. On Linux, the container user's GID/UIDs
# will be updated to match your local UID/GID (when using the dockerFile property).
# See https://aka.ms/vscode-remote/containers/non-root-user for details.
ARG USERNAME=dev
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Create the user
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    #
    # [Optional] Add sudo support. Omit if you don't need to install software after connecting.
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# [Optional] Set the default user. Omit if you want to keep the default as root.
USER $USERNAME

# Commands ran past this point will be ran as the redsky user
