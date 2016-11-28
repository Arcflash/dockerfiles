# VERSION 2.0
# AUTHOR: Matthieu arcflash,based on  "Puckel_" Roisil's azkaban image
# "Puckel_" Roisil's DOCKER HUB: https://hub.docker.com/u/puckel/
# "Puckel_" Roisil's SOURCE: https://github.com/puckel/docker-azkaban
# DESCRIPTION: Simple Debian image for azkaban-executor based on official java:8
# BUILD: docker build --rm -t puckel/azkaban-executor .
# SOURCE: https://github.com/puckel/docker-azkaban

FROM java:8
MAINTAINER arcflash 

# Never prompts the user for choices on installation/configuration of packages
ENV DEBIAN_FRONTEND noninteractive
ENV TERM linux
# Work around initramfs-tools running on kernel 'upgrade': <http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=594189>
ENV INITRD No

ENV AZK_VERSION 2.5.0
ENV MYSQL_JDBC_VERSION 5.1.35

#WORKDIR /root
WORKDIR /root/azkaban

#unknown parameter -yqq,consider we use centos,not ubuntu,annotation these commands
RUN #apt-get update -yqq \
    #&& apt-get install -yqq \
    curl \
    && curl -sLk http://pan.baidu.com/s/1jIiBenG#list/path=%2F/azkaban-executor-server-$AZK_VERSION.tar.gz| tar xz \
    && curl -sLk http://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-$MYSQL_JDBC_VERSION.tar.gz| tar xz \
    && mv mysql-connector-java-$MYSQL_JDBC_VERSION/mysql-connector-java-$MYSQL_JDBC_VERSION-bin.jar azkaban-executor-$AZK_VERSION/extlib/ \
    && rm -rf mysql-connector-java-$MYSQL_JDBC_VERSION \
    # Work around to run container as a daemon
    && sed -i "s/&//" azkaban-executor-$AZK_VERSION/bin/azkaban-executor-start.sh 
#    && apt-get clean
#    && apt-get clean \
#    && rm -rf \
#    /var/lib/apt/lists/* \
#    /tmp/* \
#    /var/tmp/* \
#    /usr/share/man \
#    /usr/share/doc \
#    /usr/share/doc-base

ADD conf/azkaban.properties azkaban-executor-$AZK_VERSION/conf/azkaban.properties

# Azkaban executor port
EXPOSE 12321

# Define default workdir
WORKDIR /root/azkaban/azkaban-executor-$AZK_VERSION

CMD ["bin/azkaban-executor-start.sh"]

http://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.35.tar.gz