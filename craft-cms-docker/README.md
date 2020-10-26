This folder explores creating a Dockerized Craft CMS project.

# Getting started

First, let's create a new directory to hold the source files for our Craft CMS project.

```sh
# Create a directory for our Craft CMS source files
$ mkdir src

# Use composer to create a basic Craft CMS project
$ cd src
$ docker run --rm -v $(pwd):/app composer create-project craftcms/craft .
```
