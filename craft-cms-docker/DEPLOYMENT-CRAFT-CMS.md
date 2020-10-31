# Our goal

This guide will explore deployment and hosting possibilities for our Craft CMS project.

Our goal is to arrive at a solution that will allow us to:

- Develop and enhance a headless Craft CMS back-end
  - NOTE: GraphQL capabilities are only available once the user [upgrades to Craft Pro](https://craftcms.com/pricing)
- Serve Craft CMS content to client applications
- Deploy Craft CMS code to separate environments (e.g., development, staging, hotfixes, etc.)
- Have the ability to manage and revert
  - PHP configuration and changes between environments
  - Craft CMS plugins between environments
  - Database schema and optionally data between environments

## Hosting

### Hyperlane

The first hosted Craft CMS provider I looked at was [Hyperlane](https://hyperlane.co).

#### TL:DR

While there may be a few growing pains with initial setup and configuration, the ease of transferring settings fluidly between environments is a huge win. Craft CMS can run as a GraphQL back-end - serving content from all three environments.

Content creators can log in to the admin panel and freely create content, add plugins, customize Craft CMS, etc.

Application developers can consume the GraphQL endpoint to present Craft CMS content as desired.

#### Pros

- Each Craft CMS hosting plan includes
  - Three environments for your Craft CMS application - `Development,` `Staging,` and `Production.`
  - Automated CI/CD deployment to a Development environment
  - An ability to selectively clone Craft CMS application code, MySQL databases, or Craft CMS content freely between environments
    - This might be a point of concern. However, given server settings and database changes can occur outside of the Craft CMS codebase, this is extremely useful.

#### Concerns

- Because they are based overseas and are on CEST time, support requests will have a noticeable lag in responsiveness.
- There is a significant bug in their one-click install image that requires support to resolve during initial setup and configuration
- The GitLab CI/CD repo and integration have Craft CMS and its related services at the root - which would make any additional client applications (Next.js, etc.) appear as being related to Craft CMS codebase and not as distinct entities. Not a deal-breaker, but I could see that being a nitpicky frustration one might have as a developer.
- Database backups are self-managed

### Servd

[Servd](https://servd.host/) is partnered with both Digital Ocean and Cloudflare - a huge DevOps win without the need for a DevOps budget.

#### TL:DR

We found a winner 🏆

[Servd](https://servd.host/) is enticing from the get-go. I was impressed to see that you can specify a source repository to import (GitHub, GitLab, and Bitbucket are supported).

A new repo has been created at [https://github.com/TheRobBrennan/demo-headless-craft-cms](https://github.com/TheRobBrennan/demo-headless-craft-cms) - containing a project intended to serve as the monorepo for this solution, which includes:

- A Dockerized Craft CMS project
- An example Next.js with TypeScript application

#### Pros

- Each Servd Craft CMS hosting plan includes
  - Staging and production environments
  - Automated backups that can be restored with a single click
  - Automated load balancing across multiple instances of your Craft CMS solution
  - Asset management and optimization
  - Static caching
  - Git deployment workflows
  - Your project runs on its internal network and can only receive traffic through the hardware firewall
  - SSL encryption is provided by default, and all database data is encrypted at rest
  - Proactive infrastructure monitoring and PHP crash detection
  - 1 click restores of database, asset, codebase, and even environment settings
- Support was extremely responsive
  - Suggested joining the Craft CMS Discord Server at [https://craftcms.com/discord](https://craftcms.com/discord)

#### Enhancements

Servd can transform and optimize all of your images off-server and in the cloud. All you need to do is install the [Servd Assets and Helpers](https://plugins.craftcms.com/servd-asset-storage) plugin.
