FROM ariya/centos6-oracle-jre7

MAINTAINER Santiago Esteva <santiagoesteva@gmail.com>

ADD setup-agent.sh /setup-agent.sh

# Enable Epel repo to get nodejs/npm
RUN yum -y install epel-release
RUN yum -y update

RUN chmod +x /setup-agent.sh

RUN yum -y install sudo nodejs wget unzip gcc gcc-c++ kernel-devel tar unzip git httpd xorg-x11-server-Xvfb firefox
RUN useradd -d /home/teamcity -m -s /bin/bash -p 123456 teamcity
RUN echo -e "teamcity\tALL=(ALL)\tNOPASSWD: ALL\n" >> /etc/sudoers

# Install Node.js
RUN \
  npm install -g npm && \
  echo -e '\n# Node.js\nexport PATH="node_modules/.bin:$PATH"' >> /root/.bashrc

RUN \
  npm install -g grunt grunt-cli bower

EXPOSE 9090

USER teamcity

CMD sh -c "TEAMCITY_SERVER=$TEAMCITY_SERVER bash /setup-agent.sh run"


