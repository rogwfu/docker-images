############################################################
# Dockerfile to build Ubuntu 12.04 custom container images
# Based on Ubuntu
############################################################

# Set the base image to Ubuntu
FROM ubuntu:12.04

# File Author / Maintainer
MAINTAINER Roger Seagle 

# Update the repository sources list
RUN apt-get update

# Install Git 
RUN apt-get install -y git-core 

# Configure git to not verify https
RUN git config --global http.sslVerify false

# Install ruby dependencies
RUN apt-get install -y curl libgdbm-dev libncurses5-dev automake libtool bison libffi-dev build-essential sudo

# Add build user
RUN useradd -ms /bin/bash wopr

# Add user to sudo
RUN adduser wopr sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# Create builds directory for wopr user
RUN mkdir /builds
RUN chmod 777 /builds

# Switch user
USER wopr

# Install rvm & ruby 2.2.3
RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
RUN cd /tmp && curl -sSL https://get.rvm.io | bash -s stable
RUN echo 'source /home/wopr/.rvm/bin/rvm' >> ~/.bashrc 
RUN /bin/bash -l -c "rvm requirements"
RUN /bin/bash -l -c "rvm install 2.2.3 --disable-binary"
RUN /bin/bash -l -c "rvm use 2.2.3 --default"
RUN echo "gem: --no-ri --no-rdoc" > ~/.gemrc
RUN /bin/bash -l -c "gem install bundler"

# Set the work dir
WORKDIR /home/wopr

# overwrite this with 'CMD []' in a dependent Dockerfile
CMD ["/bin/bash"]
