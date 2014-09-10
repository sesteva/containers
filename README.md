If you want to use these images, you do not need to clone this project. 
Images are published to docker registry. 
Make sure you have docker installed and proceed.

## Pulling Images

    docker pull sesteva/yeoman
    docker pull sesteva/grunt-angular
    docker pull sesteva/grunt-polymer
	docker pull japanvik/deployd

## Creating a new Instance
Example: build and run an existing angular grunt project
First we checkout the repo:

    mkdir -p ~/Projects/Personal/muzza
    cd ~/Projects/Personal/muzza
    git clone https://github.com/unexpectedprofit-org/muzza.git

Then we instantiate a new grunt_angular box

    docker run --name muzza -p 9000:9000 -v ~/Projects/Personal/muzza:/home/project -i -t sesteva/grunt_angular

Parameters Explanation:

- name muzza -> name our instance 'muzza'
- p 9000:9000  -> forward port 9000 on port on 9000
- v HOST_PROJECT_PATH:CONTAINER_PROJECT_PATH -> we allocate the project's folder inside the container.
- i -> Keep STDIN open even if not attached 
- t -> llocate a pseudo-tty
- grunt_angular -> container image being used

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
    docker push sesteva/grunt_polymer

### Yeoman  + Angular box

    cd /grunt-angular
    docker build -t sesteva/grunt_angular .
    docker push sesteva/grunt_angular
