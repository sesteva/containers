FROM ariya/centos6-teamcity-agent

MAINTAINER Santiago Esteva <santiagoesteva@gmail.com>

RUN yum -y install wget unzip sudo gcc gcc-c++ kernel-devel tar

RUN cd /tmp && \
    wget http://nodejs.org/dist/node-latest.tar.gz && \
    tar xvzf node-latest.tar.gz && \
    rm -f node-latest.tar.gz && \
    cd node-v* && \
    ./configure && \
    CXX="g++ -Wno-unused-local-typedefs" make && \
    CXX="g++ -Wno-unused-local-typedefs" make install && \
    cd /tmp && \
    rm -rf /tmp/node-v* && \
    npm install -g npm grunt-cli bower

RUN adduser teamcity

EXPOSE 9090

CMD sudo -u teamcity -s -- sh -c "TEAMCITY_SERVER=$TEAMCITY_SERVER bash /setup-agent.sh run"


