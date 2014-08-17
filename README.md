## Setup

    mkdir -p /Projects/Docker
    cd /Projects/Docker
    git clone https://github.com/sesteva/containers.git

### Debian Base box 

    cd /debian-base
    docker build -t base_debian .

### Yeoman Ready box

    cd /node-bower-grunt-sass-yeoman
    docker build -t yeoman .

### Yeoman  + Angular box

    cd /grunt-angular
    docker build -t grunt_angular .

## Creating a new Instance
Example: build and run an existing angular grunt project
First we checkout the repo:

    mkdir -p ~/Projects/Personal/muzza
    cd ~/Projects/Personal/muzza
    git clone https://github.com/unexpectedprofit-org/muzza.git

Then we instantiate a new grunt_angular box

    docker run --name muzza -p 9000:9000 -v ~/Projects/Personal/muzza:/home/project -i -t grunt_angular

- name muzza -> name our instance 'muzza'
- p 9000:9000  -> forward port 9000 on port on 9000
- v HOST_PROJECT_PATH:CONTAINER_PROJECT_PATH -> we allocate the project's folder inside the container.
- i -> Keep STDIN open even if not attached 
- t -> llocate a pseudo-tty
- grunt_angular -> container image being used









docker run --name muzza -p 9000:9000 -v ~/Projects/Personal/muzza:/home/project -i -t grunt_angular
