# MONO Web Node
 
**Overview**

This Dockerfile builds a Debian based MONO + Apache Web node.
Designed as a standard image for the publishing step of a jenkins pipeline.

**Features**

- Based on The latest Docker Mono release (at the time of writing) is: v5.20.1
- Compatible with Auto-scaling services.
- Uses Apache mod_mono with port 80 exposed, the mono-fastcgi-server4 loads the application from /var/www.

### Base docker image

    mono:latest

### Usage

First you need to pull the image:

    docker pull 0urob0r0s/docker-mono-apache

Then build your project > create a Dockerfile > copy the application to /var/www

    FROM 0urob0r0s/docker-mono-apache
    ADD buildOutput/website /var/www/
    CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

Build your container

    docker build -t my_website .

Run it, forwarding the host's port 8080 to the container's port 80

    docker run --rm -i -t -p 8080:80 my_website

You should now be able to access the site on [your local machine port 8080](http://localhost:8080/)
