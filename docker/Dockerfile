# based on ubuntu:18.04
FROM buildbot/buildbot-worker:master

# Switch to root to be able to install stuff
USER root

# This will make apt-get install without question
ARG DEBIAN_FRONTEND=noninteractive

# Install packages
RUN apt-get -yqq update \
    && apt-get -yqq install \
        python3 \
        python3-pip \
        curl \
        git \
        golang-docker-credential-helpers 

# Install docker
WORKDIR /home/
RUN curl -fsSL https://get.docker.com -o get-docker.sh \
    && sh get-docker.sh

# Allow buildbot user to use docker
RUN groupadd docker \
    ; usermod -aG docker buildbot

# Install txrequests for to allow interaction with GitHub REST API
# In order to use  GitHubStatusPush
RUN pip3 install txrequests

# Switch to regular user for security reasons
USER buildbot
WORKDIR /buildbot

CMD ["/usr/bin/dumb-init", "twistd", "--pidfile=", "-ny", "buildbot.tac"]