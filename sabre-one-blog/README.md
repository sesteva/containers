## Build and Deploy Blog automatically

This one has not been turned into an automatic build since it contains hardcoded repo.


    git clone thisRepo
    cd sabre-one-blog
    sudo docker build --no-cache -t local/sabre-one-blog .
    sudo docker run --name blog --rm -p 4000:80 local/sabre-one-blog

We want to take advantage of cached based image but we want to avoid getting cached git repo.
That's why we use the nocahe option at the end.

Now you can access the site at localhost:4000/blog

## Deploying As daemon

    sudo service docker start
    git clone this Dockerfile folder
    cd this folder
    sudo docker build --no-cache -t local/sabre-one-blog .
    sudo docker stop blog
    sudo docker rm blog
    sudo docker run -d --name blog -p 4000:80 local/sabre-one-blog
