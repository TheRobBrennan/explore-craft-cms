# Getting started

## Local development

To develop this application on your machine, you will need to have Docker and `docker-compose` installed.

If you are unfamiliar with Docker, don't panic. You can download and install [Docker Desktop](https://www.docker.com/products/docker-desktop) - available for macOS and Windows.

### Docker scripts

This project also contains several scripts to simplify developing your application using Docker.

If you have [Node.js](https://nodejs.org/en/) installed on your system, you'll be able to run scripts in `package.json` with `npm run <script-name>` - such as `npm run start:clean`

If you don't have [Node.js](https://nodejs.org/en/) or `npm` installed, you can run the `docker-compose` commands directly. For example, instead of `npm run start:clean`, you would use `docker-compose up --build` instead.

The following scripts are in `package.json` for convenience:

- `build` - This starts the buildchain container using the latest image on your machine
- `build:clean` - This starts the buildchain container with a freshly built Docker image
- `start` - This starts the entire Dockerized application - all services defined in `docker-compose.yml` - using the latest images on your machine
- `start:clean` - This starts the entire Dockerized application - all services defined in `docker-compose.yml` - with freshly built Docker images
- `stop` - This stops all services defined in `docker-compose.yml`
- `destroy` - This removes all stopped containers (services) as defined in `docker-compose.yml`

TL:DR Any script with a `:clean` as part of the name will build a fresh Docker image for each service defined in `docker-compose.yml` before starting the application.

### Start the application

Once your development environment is configured, you can start the entire application by running either `npm run start` or `docker-compose up` 🤓

The Craft CMS web application can be viewed at [http://localhost](http://localhost)

The Craft CMS Control Panel can be viewed at [http://localhost/admin/](http://localhost/admin/)
