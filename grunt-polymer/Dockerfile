FROM sesteva/yeoman

RUN npm install -g generator-polymer

RUN mkdir -p /home/yeoman/project && \
    chmod 777 -R /home/yeoman/project

CMD cd /home/yeoman/project && \
    npm install && \
    bower install --allow-root && \
    grunt serve

RUN adduser --disabled-password --gecos "" yeoman; \
  echo "yeoman ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

ENV HOME /home/yeoman

USER yeoman

WORKDIR /home/yeoman

EXPOSE 9000
