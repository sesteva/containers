FROM dockerfile/nodejs-bower-grunt

RUN apt-get update --fix-missing && apt-get install -y ruby1.9.1-dev

RUN gem install sass compass && \
    npm install -g yo

RUN adduser --disabled-password --gecos "" yeoman; \
  echo "yeoman ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

ENV HOME /home/yeoman

USER yeoman

WORKDIR /home/yeoman

