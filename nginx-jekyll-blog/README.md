GOAL: Nginx-Jekyll blog base container with github-pages jekyll jekyll-redirect-from kramdown rdiscount rouge

    sudo docker build -t local/nginx-jekyll-blog .

You can use this image if you want to pass in folder containing a jekyll already processed blog

    sudo docker run --name blog --rm -v /home/myblog/_site:/srv/www/_site  -p 4000:80 local/nginx-jekyll-blog

Another option would be to pass blog main folder and execute jekyll build && nginx

Or...you can create your own Dockerfile and automatically build/deploy a site

    FROM sesteva/nginx-jekyll-blog

    ## Build and move to nginx
    RUN \
        cd /tmp && \
        git clone https://github.com/sesteva/blog.git blog && \
        cd blog && \
        jekyll build && \
        mv /tmp/blog/_site /srv/www
