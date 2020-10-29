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

## Create a Docker compose file

Let's define a `docker-compose.yml` file to have a set of containers executed as a single set. Note how we are specifying hostnames such as `php`, `nginx`, and `database`. This will allow our Dockerized app to refer to specific hosts within this configuration. Remember where we had "fastcgi_pass php:9000;" in our nginx configuration? This is where the hostname `php` is defined. 🤓

One crucial enhancement here is that we have mounted a shared `cpresources` directory in our `php` and `nginx` containers. This was necessary because our application assumes that our web server and PHP server both have access to the same filesystem - which is not the case when they are split into separate containers. By mounting that shared `cpresources` directory, we give the `nginx` container access to any changes or writes from our `php` container.

Please see `craft-cms-docker/docker-compose.yml` for additional details about our Docker compose file.

## Start the Craft CMS project

With our Docker compose file defined, we can start our application:

```sh
# Start the application - See https://docs.docker.com/compose/reference/overview/ for more details of the docker-compose CLI
$ docker-compose up

# OPTIONAL: If you would like to force a fresh build of the images and containers before starting the application
$ docker-compose up --build
```

You should be able to see the Craft CMS installation page at [http://localhost/admin/](http://localhost/admin/).

Feel free to play around with your Dockerized app 🤓

When done, press `CTRL+C` to stop the containers.

```sh
# If you would like to stop your application and keep the containers intact next time you start the project
$ docker-compose stop

# If you would like to destroy and remove the containers created by Docker compose
$ docker-compose rm
```

# Install and configure Craft CMS

If you have followed the _Getting Started_ instructions, your Craft CMS application is ready to be installed and configured.

## Install Craft CMS

You should be able to see the Craft CMS installation page at [http://localhost/admin/](http://localhost/admin/).

Follow the instructions provided by the installation wizard. When finished, you will be at the main dashboard to configure your Craft CMS project.

## Set up an asset source for image uploads

Notice that our `docker-compose.yml` has our `./src/web` directory mounted in the `nginx` and `php` containers. This is so that any files that are written by PHP to this folder will actually be written to our host filesystem and immediately available in our `nginx` container.

To define an asset volume, navigate from the Craft CMS dashboard to `Settings > Content - Assets > Volumes` and then click on `+ New volume`

Create a new asset volume with the following settings:

- Name: `Local`
- Handle: `local`
- Assets in this volume have public URLs: `Enabled`
- Base URL: `@web/images`
- File System Path: `/var/www/html/web/images`

Let's try uploading an image to our asset library. Navigate from the Craft CMS dashboard to `Assets,` make sure `Local` is selected, and then click on `Upload files`

If you can upload an image, continue to the next section. Otherwise, you may need to set relaxed permissions on your host filesystem by doing something like:

```sh
$ cd craft-cms-docker

# Make sure that our images directory is created and set relaxed permissions
$ mkdir src/web/images
$ chmod 777 src/web/images

# Ignore this folder so that we don't include test uploads as part of our source control
$ echo '*\n!.gitignore' > src/web/images/.gitignore
```
