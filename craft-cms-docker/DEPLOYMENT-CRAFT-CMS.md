# Our goal

This guide will explore deployment and hosting possibilities for our Craft CMS project.

Our goal is to arrive at a solution that will allow us to:

- Develop and enhance a headless Craft CMS back-end
  - NOTE: GraphQL capabilities are only available once the user [upgrades to Craft Pro](https://craftcms.com/pricing)
- Serve Craft CMS content to client applications
- Deploy Craft CMS code to separate environments (e.g., development, staging, hotfixes, etc.)
- Have the ability to manage and revert
  - PHP configuration and changes between environments
  - Craft CMS plug-ins between environments
  - Database schema and optionally data between environments

## Hosting

### Hyperlane

The first hosted Craft CMS provider I looked at was [Hyperlane](https://hyperlane.co).

#### TL:DR

While there may be a few growing pains with initial setup and configuration, the ease of transferring settings fluidly between environments is a huge win. Craft CMS can run as a GraphQL back-end - serving content from all three environments.

Content creators can log in to the admin panel and freely create content, add plug-ins, customize Craft CMS, etc.

Application developers can consume the GraphQL endpoint to present Craft CMS content as desired.

#### Pros

- Each Craft CMS hosting plan includes
  - Three environments for your Craft CMS application - `Development`, `Staging`, and `Production`
  - Automated CI/CD deployment to a Development environment
  - An ability to selectively clone Craft CMS application code, MySQL databases, or Craft CMS content freely between environments
    - This might be a point of concern. However, given that server settings and database changes can occur outside of the Craft CMS codebase, this is extremely useful.

#### Concerns

- Because they are based overseas and are on CEST time, support requests will have a noticeable lag in responsiveness.
- There is a significant bug in their one-click install image that requires support to resolve during initial setup and configuration
- The GitLab CI/CD repo and integration have Craft CMS and its related services at the root - which would make any additional client applications (Next.js, etc.) appear as being related to Craft CMS codebase and not as distinct entities. Not a deal-breaker, but I could see that being a nitpicky frustration one might have as a developer.
- Database backups are self-managed
