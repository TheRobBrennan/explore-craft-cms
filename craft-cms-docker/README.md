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
