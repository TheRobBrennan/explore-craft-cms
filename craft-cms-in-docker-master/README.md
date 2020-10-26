# Craft CMS in Docker

A git repo which follows along with the steps outlined in my "A Craft CMS Development Workflow With Docker" article series.

https://mattgrayisok.com/a-craft-cms-development-workflow-with-docker-part-1-local-development

## Branches

The `master` branch will always contain the latest version of a Craft CMS in Docker project as it stands at the end of the article series.

Each article in the series also has a dedicated branch named `part-x` which represents the state of the project at the conclusion of that article.

Finally there are several `add-on` branches which demonstrate some of the additional functionality described in other articles outside of the main article series.

## Getting Started

* Make sure you have docker and docker-compose installed. [Some super quick instructions](https://mattgrayisok.com/simplest-way-to-install-docker)
* Clone this repo `git clone git@gitlab.com:mattgrayisok/craft-cms-in-docker.git`
* Run `docker-compose up`
* Visit `http://localhost`
* Edit files in `src`
