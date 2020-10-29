# Source - https://mattgrayisok.com/a-craft-cms-development-workflow-with-docker-part-2-buildchains-in-docker
FROM node:8.16

# This command installs yarn and is optional if you just prefer to use npm everywhere
RUN apt-get update && apt-get install -y apt-transport-https \
  && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
  && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
  && apt-get update \
  && apt-get install -y yarn

# Set the working directory in our container
WORKDIR /project

# Copy our buildchain's package.json file into the working directory
COPY ./docker-config/buildchain/package.json package.json

# Make sure we're in the right directory and use yarn to install our files
RUN cd /project && yarn install

# Build our assets
CMD yarn run build