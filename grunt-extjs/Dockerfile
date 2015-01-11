FROM sesteva/yeoman

RUN npm install -g generator-extjs coffee-script

RUN mkdir -p /home/yeoman/project && \
    chmod 777 -R /home/yeoman/project

CMD cd /home/yeoman/project && \
    npm install && \
    bower install --allow-root && \
    grunt serve

EXPOSE 9000

