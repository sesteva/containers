If you want to use these images, you do not need to clone this project. 
Images are published to docker registry. 
Make sure you have docker installed and proceed.

## Behind Proxy

1- update /etc/default/docker 

export http_proxy="http://127.0.0.1:3128/"

2- When running the daemon

sudo HTTP_PROXY=http://localhost:3128/ docker -d &

3- In your dockerfile or when you run the container. This will be need by npm/bower
    
    export http_proxy="http://172.17.42.1:3128/"
    export https_proxy="http://172.17.42.1:3128/"
    npm config set https-proxy http://172.17.42.1:3128 
    git config --global url."https://".insteadOf git://

TODO: automate these!

# Linux
I have a squid instance running on the host on port 3128

    iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to 3128
   
I also had to update my squid config to allow the requests from docker ip range

    acl dtslocalnet dst 172.17.0.0/24

## Pulling Images

    docker pull sesteva/grunt-sass-cofee
    docker pull sesteva/grunt-project
    docker pull sesteva/centos6-teamcity-agent-nodejs

Out of Order due to yeoman not running on root

    docker pull sesteva/yeoman
    docker pull sesteva/grunt-angular
    docker pull sesteva/grunt-polymer
    docker pull sesteva/grunt-extjs


## Third Party Interesting Containers

     docker pull sesteva/private-bower
     docker pull sesteva/deployd
     docker pull keyvanfatehi/sinopia:0.12.0
     docker pull ariya/centos6-teamcity-server
     docker pull ariya/centos6-teamcity-agent


### TeamCity

For teamcity take a look at this article: http://ariya.ofilabs.com/2014/07/easy-teamcity-installation-with-docker.html

TeamCity Server
     
     sudo docker run -dt -name teamcity_server -p 8111:8111 ariya/centos6-teamcity-server

TeamCity Agent
     
     sudo docker run -e TEAMCITY_SERVER=http://172.17.42.1:8111 --name teamcity_agent-01 --link teamcity_server:teamcity_server -dt ariya/centos6-teamcity-agent

TeamCity Agent with Nodejs Grunt cli bower

     sudo docker run -e TEAMCITY_SERVER=http://172.17.42.1:8111 --name teamcity_agent-02 --link teamcity_server:teamcity_server -dt sesteva/centos6-teamcity-agent-nodejs


### Deployd

     docker run --name deployd -p 2403:2403 -i -t sesteva/deployd
     open browser http://localhost:2403/dashboard

## Creating a new Grunt-Project

### Using Yeoman

Yeoman does not play very well with ROOT inside docker.
To ease the pain, you should use yeoman outside and the use the docker environment to build/test/run.
Since Yeoman should be used to create files this should not be a problem.

#### Requirements On your HOST

- Docker & Nsenter
- Nodejs

 Copy/Past and execute:

     cd /tmp && \
     wget http://nodejs.org/dist/node-latest.tar.gz && \
     tar xvzf node-latest.tar.gz && \
     rm -f node-latest.tar.gz && \
     cd node-v* && \
     ./configure && \
     CXX="g++ -Wno-unused-local-typedefs" make && \
     sudo CXX="g++ -Wno-unused-local-typedefs" make install && \
     cd /tmp && \
     rm -rf /tmp/node-v* && \
     sudo npm install -g npm

 Add to your .bashrc

     # Node.js
     export PATH="node_modules/.bin:$PATH"

 Now run

     source ~/.bashrc
     node -v
     npm -v

- Bower

     sudo npm install -g bower

- Yo

     sudo npm install -g yo

- Your specific yeoman generator

     sudo npm install -g generator-polymer generator-extjs generator-angular

##### Option 1 - New Project Flow

    cd Projects
    mkdir newProject
    cd newProject
    yo

Follow yeoman instructions to set it up

##### Option 2 - Existing Project

    cd Projects
    git clone github....newProject.git
    cd newProject


#### Build, Test, Run - Docker

##### Option 1

    sudo docker run --name projectName -p 9000:9000 -v ~/Projects/newProject:/home/project -i -t sesteva/grunt-project

This will map your local folder into a project folder inside the container. It will run npm, bower and grunt serve.

##### Option 2

    sudo docker run --name projectName -p 9000:9000 -v ~/Projects/newProject:/home/project -it sesteva/grunt-project /bin/bash

This option overrides the default action (npm install, bower install, grunt serve) and it lets you access the command line.

Parameters Explanation:

- name projectName -> name our instance 'projectName'
- p 9000:9000  -> forward port 9000 on port on 9000
- v HOST_PROJECT_PATH:CONTAINER_PROJECT_PATH -> we allocate the project's folder inside the container.
- i -> Keep STDIN open even if not attached
- t -> allocate a pseudo-tty
- grunt_project -> container image being used

#### Access the container

requirements - nsenter

    sudo docker run --rm -v /usr/local/bin:/target jpetazzo/nsenter

Now we can use nsenter to access a running container

    sudo docker-enter projectName /bin/bash

## Containers Setup

    mkdir -p /Projects/Docker
    cd /Projects/Docker
    git clone https://github.com/sesteva/containers.git

Builds are already set in docker public registry as automated builds. 
If you were to push them manually, thats when you execute last command 'docker push'

### Debian Base box 

    cd /debian-base
    docker build -t sesteva/base_debian .
    docker push sesteva/base_debian

### Yeoman Ready box

    cd /node-bower-grunt-sass-yeoman
    docker build -t sesteva/yeoman .
    docker push sesteva/yeoman

### Yeoman + Polymer box

    cd /grunt-polymer
    docker build -t sesteva/grunt_polymer .
    docker push sesteva/grunt-polymer

### Yeoman  + Angular box

    cd /grunt-angular
    docker build -t sesteva/grunt_angular .
    docker push sesteva/grunt-angular

### Deployd box

    cd /deployd
    docker build -t sesteva/deployd .
    docker push sesteva/deployd

    

