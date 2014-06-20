# VERSION 0.1
# To build:
# 1. Install docker (http://docker.io)
# 2. Build container: docker build .


FROM    ubuntu:14.04
MAINTAINER Stefan Gordon


# Install NodeJS
RUN     apt-get install -y nodejs

# Install legacy support for 'node' command
RUN     apt-get install nodejs-legacy

# Install NPM
RUN     apt-get install -y npm

# Install MongoDB
RUN     apt-get install -y mongodb

# Install GIT
RUN     apt-get install -y git

# Install WGET
RUN     apt-get install -y wget

# Clone Nitrogen service
RUN     git clone https://github.com/nitrogenjs/service /home/nitrogen

# Pull down Nitrogen NodeJS dependencies
RUN     cd /home/nitrogen; npm cache clean; npm install

# Install Redis
RUN \
  cd /tmp && \
  wget http://download.redis.io/redis-stable.tar.gz && \
  tar xvzf redis-stable.tar.gz && \
  cd redis-stable && \
  make && \
  make install && \
  cp -f src/redis-sentinel /usr/local/bin && \
  mkdir -p /etc/redis && \
  cp -f *.conf /etc/redis && \
  rm -rf /tmp/redis-stable* && \
  sed -i 's/^\(bind .*\)$/# \1/' /etc/redis/redis.conf && \
  sed -i 's/^\(daemonize .*\)$/# \1/' /etc/redis/redis.conf && \
  sed -i 's/^\(dir .*\)$/# \1\ndir \/data/' /etc/redis/redis.conf && \
  sed -i 's/^\(logfile .*\)$/# \1/' /etc/redis/redis.conf

# Define mountable directories.
VOLUME ["/data"]

# Define working directory.
WORKDIR /home/nitrogen

# Expose ports
EXPOSE  3050 9000

ADD run /home/nitrogen/

RUN     chmod +x /home/nitrogen/run

CMD ["/home/nitrogen/run"]

