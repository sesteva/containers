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

    docker pull sesteva/yeoman
    docker pull sesteva/grunt-angular
    docker pull sesteva/grunt-polymer
    docker pull sesteva/grunt-extjs
    docker pull sesteva/private-bower
    
## Third Party Interesting Containers
     
     docker pull sesteva/deployd
     docker pull keyvanfatehi/sinopia:0.12.0
     
For teamcity take a look at this article: http://ariya.ofilabs.com/2014/07/easy-teamcity-installation-with-docker.html     

TeamCity Server
     
     sudo docker run -dt -name teamcity_server -p 8111:8111 ariya/centos6-teamcity-server

TeamCity Agent
     
     sudo docker run -e TEAMCITY_SERVER=http://172.17.42.1:8111 --name teamcity-agent-01 --link teamcity_server:teamcity_server -it ariya/centos6-teamcity-agent


## Creating a new Instance
Example: build and run an existing angular grunt project
First we checkout the repo:

    mkdir -p ~/Projects/Personal/muzza
    cd ~/Projects/Personal/muzza
    git clone https://github.com/unexpectedprofit-org/muzza.git

Then we instantiate a new grunt_angular box

    docker run --name muzza -p 9000:9000 -v ~/Projects/Personal/muzza:/home/yeoman/project -i -t sesteva/grunt-angular

Parameters Explanation:

- name muzza -> name our instance 'muzza'
- p 9000:9000  -> forward port 9000 on port on 9000
- v HOST_PROJECT_PATH:CONTAINER_PROJECT_PATH -> we allocate the project's folder inside the container.
- i -> Keep STDIN open even if not attached 
- t -> llocate a pseudo-tty
- grunt_angular -> container image being used

### Other boxes

    docker run --name deployd -p 2403:2403 -i -t sesteva/deployd
    open browser http://localhost:2403/dashboard



## Send commands to container with Nsenter

	docker run --rm -v /usr/local/bin:/target jpetazzo/nsenter

	# list the root filesystem
	docker-enter my_awesome_container ls -la


## Building for the first time

This is only executed if the image is not public in docker registry.

## Setup

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

    

