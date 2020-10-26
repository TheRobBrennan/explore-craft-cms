This folder explores creating a Dockerized Craft CMS project.

# Getting started

## Create a Craft CMS project using Docker and composer

First, let's create a new directory to hold the source files for our Craft CMS project.

```sh
# Create a directory for our Craft CMS source files
$ mkdir src

# Use composer to create a basic Craft CMS project
$ cd src
$ docker run --rm -v $(pwd):/app composer create-project craftcms/craft .
```

## Create Docker containers for our new Craft CMS project

We will be creating Docker containers to house the main configuration scripts for each container and any other scripts or assets they need. This enables us to keep our Docker configuration and related files separate from our Craft CMS application.

```sh
# Make sure we're in the craft-cms-docker folder and not the `./craft-cms-docker/src` folder
$ cd ..

# Create a directory structure for our Docker configuration files
$ mkdir -p docker-config/php
$ mkdir -p docker-config/nginx
```

### PHP

Create the Dockerfile for our PHP container at `docker-config/php/Dockerfile`. This container's sole responsibility is to run `php-fpm` - which will parse our PHP files and return appropriate responses.

One benefit of creating our PHP image in this manner is that we can do other things with it down the line - such as mounting temporary test code, deploying to different environments, etc.

### nginx

Create the Dockerfile for our nginx container at `docker-config/nginx/Dockerfile`. This container will use nginx to respond to incoming traffic, respond immediately with a static file, or pass the request on to our PHP container.

#### Custom nginx configuration

We need to override the default nginx configuration to have it forward certain requests to our PHP container. Please see `docker-config/nginx/default.conf` for more details.

The default configuration we are specifying is a pretty standard setup where an nginx server should attempt to server requests using files from the local disk and, if no matching file can be found, transform the request into a request for `index.php` and forward the request to another host/port using fastCGI.

The most important piece for us to focus on is this line - where we are passing the request to our PHP container.

```
fastcgi_pass php:9000;
```
