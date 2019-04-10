FROM ubuntu:16.04

MAINTAINER paul.marinas@gmail.com

ENV BASEDIR=/usr/lib/unifi \
  DATADIR=/var/lib/unifi \
  RUNDIR=/var/run/unifi \
  LOGDIR=/var/log/unifi \
  JVM_MAX_HEAP_SIZE=1024M \
  JVM_INIT_HEAP_SIZE=1024M \
  JAVA_HOME=/usr/lib/jvm/java-8-oracle

RUN apt-get update \
  && apt-get install -y \
    python-software-properties \
    apt-utils \
    software-properties-common \
    apt-transport-https \
    ca-certificates

RUN add-apt-repository -y ppa:webupd8team/java
RUN apt-get update
RUN echo debconf shared/accepted-oracle-license-v1-1 select true |  debconf-set-selections
RUN echo debconf shared/accepted-oracle-license-v1-1 seen true |  debconf-set-selections
RUN apt-get -y --force-yes --no-install-recommends install oracle-java8-installer
RUN apt-get -y --force-yes --no-install-recommends install oracle-java8-set-default
RUN apt-get -y install oracle-java8-installer
RUN apt-get -y install jsvc joe mc tcpdump lynx haveged net-tools

#unifi install
RUN  apt-key adv --keyserver keyserver.ubuntu.com --recv 06E85760C0A52C50 \ 
  && echo "deb http://www.ubnt.com/downloads/unifi/debian stable ubiquiti" |  tee /etc/apt/sources.list.d/ubiquiti.list \
  && apt-get update && apt-get -q -y install unifi

#mongodb install for ubuntu 14.04
RUN  apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10 \
  && echo "deb http://downloads-distro.mongodb.org/repo/debian-sysvinit dist 10gen" |  tee /etc/apt/sources.list.d/mongodb-org-3.0.list \
  && apt-get update && apt-get -q -y install \
    mongodb-org 
RUN  apt-get update


RUN /etc/init.d/haveged restart
RUN /etc/init.d/unifi restart

CMD /etc/init.d/unifi start && tail -f /dev/null
EXPOSE 6789/tcp 8080/tcp 8443/tcp 8880/tcp 8843/tcp 3478/udp
