#
# Debian Dockerfile
#
#

# Pull base image.
FROM debian:jessie

# Install.
RUN \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y build-essential && \
  apt-get install -y software-properties-common && \
  apt-get install -y byobu curl git htop man unzip vim wget

# Add files.
#ADD root/.bashrc ~/.bashrc
#ADD root/.gitconfig ~/.gitconfig
#ADD root/scripts ~/scripts

# Set environment variables.
ENV HOME /root

# Define working directory.
WORKDIR /root

#USER user

# Define default command.
CMD ["bash"]

