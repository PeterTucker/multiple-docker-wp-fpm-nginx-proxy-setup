# Multiple Wordpress FPM Setup with jwilder/nginx-proxy, Let's Encrypt SSL, and low memory mysql using docker-compose! Phew! (yes, this is the repo you've been looking for)

Maybe my **google-fu** is not up to snuff, or maybe I'm the first to figure out this setup. Regardless, in my search to find a multiple wordpress fpm docker setup I came across many other devs(**stackoverflow, reddit, github**) who while in search of the same setup all seemed to run into roadblocks. Most of the conversations I read seemed to end with a dead end, and then the devs ultimately switched to **traefik**. Understandable. I too almost gave up on this setup with **jwilder's** **nginx-proxy**.

**But Alas!** After much experimenting, I was finally able to get a multiple wordpress fpm docker setup working. I've used **WORDPRESS-FPM/NGINX & LOW-MEMORY-MYSQL** as they both are resource efficient docker images, as opposed to the docker **apache** flavor version of wordpress, and the normal mysql image.

I'm uploading this setup to github so hopefully others may find it.

## Setup:
In **wordpress/docker-compose.yml**, change out **example.com** to your URL, and **user@example.com** to your email. Change out **<MYSQL_PASSWORD>**.

If you change out the name of **"wp1_site"** in the **wordpress/docker-compose.yml** make sure you change out the name in **wordpress/nginx/nginx.conf**:
```
    fastcgi_pass wp1_site:9000;
```
In **wordpress2/docker-compose.yml**, change out **example2.com** to your URL, and **user@example.com** to your email. Change out **<MYSQL_PASSWORD>**

If you change out the name of **"wp2_site"** in the **wordpress2/docker-compose.yml** make sure you change out the name in **wordpress2/nginx/nginx.conf**
```
    fastcgi_pass wp2_site:9000;
```
## RUN:
```
docker network create nginx-proxy

cd nginx-proxy
docker-compose up -d

cd ../wordpress
docker-compose up -d

cd ../wordpress2
docker-compose up -d
```

#### Resources:
https://medium.com/swlh/wordpress-deployment-with-nginx-php-fpm-and-mariadb-using-docker-compose-55f59e5c1a

https://blog.ssdnodes.com/blog/host-multiple-ssl-websites-docker-nginx/
