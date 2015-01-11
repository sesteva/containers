# Using Yeoman

Yeoman does not play very well with ROOT inside docker.
To ease the pain, you should use yeoman outside and the use the docker environment to build/test/run.
Since Yeoman should be used to create files this should not be a problem.

## Requirements

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

## Option 1 - New Project Flow

    cd Projects
    mkdir newProject
    cd newProject
    yo

Follow yeoman instructions to set it up

Option 2 - Existing Project

    cd Projects
    git clone github....newProject.git
    cd newProject


## Build, Test, Run - Docker

Option 1

    sudo docker run --name projectName -p 9000:9000 -v ~/Projects/newProject:/home/project -i -t sesteva/grunt-project

This will map your local folder into a project folder inside the container. It will run npm, bower and grunt serve.

Option 2

    sudo docker run --name projectName -p 9000:9000 -v ~/Projects/newProject:/home/project -it sesteva/grunt-project /bin/bash

This option overrides the default action (npm install, bower install, grunt serve) and it lets you access the command line.

Parameters Explanation:

- name projectName -> name our instance 'projectName'
- p 9000:9000  -> forward port 9000 on port on 9000
- v HOST_PROJECT_PATH:CONTAINER_PROJECT_PATH -> we allocate the project's folder inside the container.
- i -> Keep STDIN open even if not attached
- t -> allocate a pseudo-tty
- grunt_project -> container image being used

### Access the container

We can use nsenter to access a running container

    sudo docker-enter projectName /bin/bash



