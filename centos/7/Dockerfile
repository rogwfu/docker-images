############################################################
# Dockerfile to build Centos 7 custom container images
# Based on Debian 
############################################################

# Set the base image to Centos 
FROM centos:7

# File Author / Maintainer
MAINTAINER Roger Seagle 

# Update the repository sources list
RUN yum -y update; yum clean all

# Install Git 
RUN yum -y install git

## Install ruby dependencies
RUN yum -y install tar which patch libyaml-devel libffi-devel glibc-headers autoconf gcc-c++ glibc-devel readline-devel zlib-devel openssl-devel bzip2 automake libtool bison fakeroot

# Configure git to not verify https
RUN git config --global http.sslVerify false

# Install rvm & ruby 2.2.3
RUN gpg2 --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
RUN cd /tmp && curl -sSL https://get.rvm.io | bash -s stable
RUN echo 'source /usr/local/rvm/scripts/rvm' >> /etc/bash.bashrc
RUN /bin/bash -l -c "rvm requirements"
RUN /bin/bash -l -c "rvm install 2.2.3 --disable-binary"
RUN /bin/bash -l -c "rvm use 2.2.3 --default"
RUN echo "gem: --no-ri --no-rdoc" > ~/.gemrc
RUN /bin/bash -l -c "gem install bundler"

# overwrite this with 'CMD []' in a dependent Dockerfile
CMD ["/bin/bash"]
