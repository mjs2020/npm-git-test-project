# Run me with
#   docker build -t npmtest-centos7 --build-arg ssh_prv_key="$(cat ~/.ssh/id_rsa)" -f centos7/Dockerfile . && docker run -it npmtest-centos7
# Then if your ssh key has a passphrase remove it:
#   ssh-keygen -p
# And finally run:
#   cd /root/npmtest
#   npm i && npm ls

FROM centos:7

# Add repos for node 8.11.2
RUN curl -sL https://rpm.nodesource.com/setup_8.x | bash -

# Update
RUN yum -y update; yum clean all

# install node 8.x.x
RUN yum -y install nodejs

RUN yum -y install  https://centos7.iuscommunity.org/ius-release.rpm
RUN yum -y install  git2u-all

# install npm 6.5.0
RUN npm i -g npm@6.5.0

# Add project
ADD . /root/npmtest

# Add SSH key from host
ARG ssh_prv_key
RUN mkdir -p /root/.ssh && \
    chmod 0700 /root/.ssh && \
    echo "$ssh_prv_key" > /root/.ssh/id_rsa && \
    chmod 600 /root/.ssh/id_rsa && \
    ssh-keyscan github.com > /root/.ssh/known_hosts

# Print versions
RUN git --version
RUN node --version
RUN npm --version