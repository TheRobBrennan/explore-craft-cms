After a cursory review of the Craft CMS guide, I was excited to see that enabling headless mode in Craft CMS is as easy as adding the following configuration setting to `craft-cms-docker/src/config/general.php`:

```php
// Run Craft CMS in headless mode - https://craftcms.com/docs/3.x/config/config-settings.html#headlessmode
'headlessMode' => true,
```

Except, of course, nothing is ever that easy. 🤓

This guide covers how to configure Craft CMS to run in headless mode.

# Getting started

To use Craft CMS as a headless CMS, we will need to create a GraphQL endpoint that our applications can access.

We have to [upgrade to Craft Pro](https://craftcms.com/pricing) to make that happen.

## Upgrade to Craft Pro

For local development, you can start the application and then navigate to [http://localhost/admin/plugin-store/upgrade-craft](http://localhost/admin/plugin-store/upgrade-craft). Select `Try for free` and then return to your dashboard at [http://localhost/admin/dashboard](http://localhost/admin/dashboard).

GraphQL should exist as an option in the left sidebar.

You can verify GraphQL has been configured correctly by executing this simple query in GraphIQL - [http://localhost/admin/graphiql?query=%7Bping%7D](http://localhost/admin/graphiql?query=%7Bping%7D). You should see a response like:

```json
{
  "data": {
    "ping": "pong"
  }
}
```

### Add a GraphQL API endpoint to Craft CMS

To set up a public endpoint for your CraftCMS GraphQL API:

```php
// Create a URL rule in config/routes.php that points to the graphql/api controller - such as 'http://localhost/graphql'
return [
    'graphql' => 'graphql/api',
    // ...
];
```

You can verify this GraphQL endpoint has been configured correctly by executing this simple query - [http://localhost/graphql?query=%7Bping%7D](http://localhost/graphql?query=%7Bping%7D). You should see a response like:

```json
{ "data": { "ping": "pong" } }
```

Please see the guide at [https://craftcms.com/docs/3.x/graphql.html#create-your-api-endpoint](https://craftcms.com/docs/3.x/graphql.html#create-your-api-endpoint) for more details.
