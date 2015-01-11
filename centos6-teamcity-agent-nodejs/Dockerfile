FROM ariya/centos6-oracle-jre7

MAINTAINER Santiago Esteva <santiagoesteva@gmail.com>

RUN yum -y install wget unzip sudo gcc gcc-c++ kernel-devel tar

ADD setup-agent.sh /setup-agent.sh
RUN yum -y install wget unzip sudo

RUN adduser teamcity && \
  sed -i -e "s/%sudo.*$/%sudo ALL=(ALL:ALL) NOPASSWD:ALL/" /etc/sudoers

RUN \
  cd /tmp && \
  wget http://nodejs.org/dist/node-latest.tar.gz && \
  tar xvzf node-latest.tar.gz && \
  rm -f node-latest.tar.gz && \
  cd node-v* && \
  ./configure && \
  CXX="g++ -Wno-unused-local-typedefs" make && \
  CXX="g++ -Wno-unused-local-typedefs" make install && \
  cd /tmp && \
  rm -rf /tmp/node-v* && \
  npm install -g npm && \
  echo -e '\n# Node.js\nexport PATH="node_modules/.bin:$PATH"' >> /root/.bashrc

RUN npm install -g grunt-cli bower

EXPOSE 9090

CMD sudo -u teamcity -s -- sh -c "TEAMCITY_SERVER=$TEAMCITY_SERVER bash /setup-agent.sh run"


