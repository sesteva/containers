FROM sesteva/nginx-jekyll-blog

## Build and move to nginx
RUN \
    cd /tmp && \
    git clone https://github.com/sesteva/blog.git blog && \
    cd blog && \
    jekyll build && \
    mv /tmp/blog/_site /srv/www