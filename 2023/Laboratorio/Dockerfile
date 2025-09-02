FROM ubuntu:latest
LABEL Author="Jose R. Hilera"

RUN apt-get -y update && \
    apt-get install -y wget && \
    apt-get install -y git && \
    apt-get install -y sudo && \
    apt-get install -y maven

# GITLAB-RUNNER
RUN wget -O /usr/local/bin/gitlab-runner https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-linux-amd64
RUN chmod 777 /usr/local/bin/gitlab-runner

# TOMCAT
EXPOSE 8080
RUN cd tmp && \
    wget http://apache.uvigo.es/tomcat/tomcat-9/v9.0.38/bin/apache-tomcat-9.0.38.tar.gz && \
    tar -zxvf /tmp/apache-tomcat-9.0.38.tar.gz -C /usr/local && \
    cd /usr/local && mv apache-tomcat-9.0.38 tomcat && \
    cd /tmp && rm -rf *

# MYSQL
EXPOSE 3306
RUN sudo DEBIAN_FRONTEND=noninteractive apt-get install -y mysql-server

# PHANTOMJS
RUN cd tmp && \
    wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2 && \
    tar xvjf /tmp/phantomjs-2.1.1-linux-x86_64.tar.bz2 && \
    mv /tmp/phantomjs-2.1.1-linux-x86_64/bin/phantomjs /usr/bin && \
    rm -rf *

CMD sudo service mysql start && sh /usr/local/tomcat/bin/catalina.sh start && /bin/bash