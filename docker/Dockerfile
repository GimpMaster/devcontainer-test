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

