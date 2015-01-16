FROM octohost/jekyll-nginx

ENV LANGUAGE en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8

WORKDIR /srv/www

RUN \
    apt-get install -y node python-pygments && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/

RUN gem install github-pages jekyll jekyll-redirect-from kramdown rdiscount rouge

EXPOSE 80

CMD nginx