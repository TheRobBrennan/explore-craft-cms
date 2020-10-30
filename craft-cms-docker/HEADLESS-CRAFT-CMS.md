After a cursory review of the Craft CMS guide, I was excited to see that enabling headless mode in Craft CMS is as easy as adding the following configuration setting to `craft-cms-docker/src/config/general.php`:

```php
// Run Craft CMS in headless mode - https://craftcms.com/docs/3.x/config/config-settings.html#headlessmode
'headlessMode' => true,
```

Except, of course, nothing is ever that easy. 🤓

This guide covers how to configure Craft CMS to run in headless mode.
