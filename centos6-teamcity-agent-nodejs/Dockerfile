FROM ariya/centos6-oracle-jre7

MAINTAINER Santiago Esteva <santiagoesteva@gmail.com>

ADD setup-agent.sh /setup-agent.sh

# Enable Epel repo to get nodejs/npm
RUN yum -y install epel-release
RUN yum -y update

RUN chmod +x /setup-agent.sh

RUN yum -y install wget unzip sudo gcc gcc-c++ kernel-devel tar unzip git nodejs httpd xorg-x11-server-Xvfb firefox
RUN npm install -g bower grunt grunt-cli

## RUN mkdir -p /usr/local/lib/selenium && wget -q -P /usr/local/lib/selenium http://selenium-release.storage.googleapis.com/2.43/selenium-server-standalone-2.43.1.jar

RUN adduser teamcity

EXPOSE 9090

CMD sudo -u teamcity -s -- sh -c "TEAMCITY_SERVER=$TEAMCITY_SERVER bash /setup-agent.sh run"


