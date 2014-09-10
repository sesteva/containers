FROM sesteva/yeoman

RUN npm install -g generator-angular coffee-script

RUN mkdir -p /home/project

CMD cd /home/project && \
    npm install && \
    bower install --allow-root && \
    grunt serve

WORKDIR /home/project

EXPOSE 9000

