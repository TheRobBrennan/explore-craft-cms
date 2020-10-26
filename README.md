This repo will explore local development with Craft CMS - with an eye towards automated CI/CD pipelines.

# Getting started

## Prerequisites

- [Docker](https://www.docker.com)
- [Composer](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-macos)

### Docker

I recommend downloading and installing [Docker Desktop](https://www.docker.com/products/docker-desktop) for macOS or Windows development.

### Composer

Composer requires PHP v5.3 or newer; however, Craft CMS v3.5.x will need to use PHP v7.0 or newer.

To install Composer, please follow the guide at [https://getcomposer.org/doc/00-intro.md#system-requirements](https://getcomposer.org/doc/00-intro.md#system-requirements).

Assuming you have PHP installed on your system, you can follow the guide at [https://getcomposer.org/download/](https://getcomposer.org/download/) containing the latest commands to download and install Composer.

```sh
# Example script verifying Composer install instructions as of this writing
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === 'c31c1e292ad7be5f49291169c0ac8f683499edddcfd4e42232982d0fd193004208a58ff6f353fde0012d35fdd72bc394') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```

This will install Composer into your current working directory. Verify that you can run it:

```sh
php composer.phar --version
# Composer version 2.0.2 2020-10-25 23:03:59

# On macOS or Linux, you can install composer globally with the following command
mv composer.phar /usr/local/bin/composer
composer --version
# Composer version 2.0.2 2020-10-25 23:03:59
```

# Resources

## A Craft CMS Development Workflow With Docker

Matt Gray wrote a great series of posts regarding Craft CMS development workflows with Docker. The `craft-cms-in-docker-master` folder reflects the latest code from his repo - last updated roughly a year ago - at [https://gitlab.com/mattgrayisok/craft-cms-in-docker](https://gitlab.com/mattgrayisok/craft-cms-in-docker).

[A Craft CMS Development Workflow With Docker: Part 1 - Local Development](https://mattgrayisok.com/a-craft-cms-development-workflow-with-docker-part-1-local-development)
