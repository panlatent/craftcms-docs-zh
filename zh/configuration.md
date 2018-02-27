# Configuration

- [PHP Constants](#php-constants)
- [General Config](#general-config)
- [Database Config](#database-config)
- [Data Caching Config](#data-caching-config)
- [Guzzle Config](#guzzle-config)
- [Aliases](#aliases)
- [Overriding Volume Settings](#overriding-volume-settings)
- [URL Rules](#url-rules)
- [Redactor Configs](#redactor-configs)
- [HTML Purifier](#html-purifier-configs)
- [Application Config](#application-config)
  - [Mailer Component](#mailer-component)

## PHP Constants

Your `web/index.php` file can specify a few PHP constants, which Craft’s bootstrap script will check for while loading and configuring Craft.

- `CRAFT_BASE_PATH` – The path to the **base directory** that Craft will look for `config/`, `templates/`, and other directories within by default. (It is assumed to be the parent of the `vendor/` directory by default.)
- `CRAFT_COMPOSER_PATH` – The path to `composer.json`. (It is assumed to live within the base directory by default.)
- `CRAFT_CONFIG_PATH` – The path to the `config/` directory. (It is assumed to live within the base directory by default.)
- `CRAFT_CONTENT_MIGRATIONS_PATH` – The path to the `migrations/` directory used to store content migrations. (It is assumed to live within the base directory by default.)
- `CRAFT_ENVIRONMENT` – The environment ID that multi-environment configs can reference when defining their environment-specific config values. (`$_SERVER['SERVER_NAME']` will be used by default.)
- `CRAFT_LICENSE_KEY_PATH` – The path that Craft should store its license key file, including its filename. (It will be stored as `license.key` within your `config/` directory by default.)
- `CRAFT_PLUGINS_PATH` – The path to the `plugins/` directory used to store manually-installed plugins. (It is assumed to live within the base directory by default.)
- `CRAFT_SITE` – The Site handle or ID that Craft should be serving from this `index.php` file.
- `CRAFT_STORAGE_PATH` – The path to the `storage/` directory. (It is assumed to live within the base directory by default.)
- `CRAFT_TEMPLATES_PATH` – The path to the `templates/` directory. (It is assumed to live within the base directory by default.)
- `CRAFT_TRANSLATIONS_PATH` – The path to the `translations/` directory. (It is assumed to live within the base directory by default.)
- `CRAFT_VENDOR_PATH` – The path to the `vendor/` directory. (It is assumed to live 4 directories up from the bootstrap script by default.)

## General Config

Craft supports several [general configuration settings](https://docs.craftcms.com/api/v3/craft-config-generalconfig.html#properties). You can override their default values in your `config/general.php` file.

```php
return [
    'devMode' => true, 
];
```

## Database Config

Craft supports several [database configuration settings](https://docs.craftcms.com/api/v3/craft-config-dbconfig.html#properties). You can override their default values in your `config/db.php` file.

## Data Caching Config

By default, Craft will store data caches in the `storage/runtime/cache/` folder. You can configure Craft to use an alternative [cache storage](http://www.yiiframework.com/doc-2.0/guide-caching-data.html#supported-cache-storage) by overriding the `cache` application component from `config/app.php`.

```php
<?php
return [
    'components' => [
        'cache' => [
            'class' => yii\caching\ApcCache::class,
            'useApcu' => true,
        ],
    ],
];
```

### Examples

Here are a couple common examples of cache storage configurations:

#### Memcached

```php
<?php
return [
    'components' => [
        'cache' => [
            'class' => yii\caching\MemCache::class,
            'useMemcached' => true,
            'username' => getenv('MEMCACHED_USERNAME'),
            'password' => getenv('MEMCACHED_PASSWORD'),
            'defaultDuration' => 86400,
            'servers' => [
                [
                    'host' => 'localhost',
                    'persistent' => true,
                    'port' => 11211,
                    'retryInterval' => 15,
                    'status' => true,
                    'timeout' => 15,
                    'weight' => 1,
                ],
            ],
        ],
    ],
];
```

#### Redis

To use Redis cache storage, you will first need to install the [yii2-redis](https://github.com/yiisoft/yii2-redis) library. Then configure Craft’s `cache` component to use it:

```php
<?php
return [
    'components' => [
        'cache' => [
            'class' => yii\redis\Cache::class,
            'defaultDuration' => 86400,
            'redis' => [
                'hostname' => 'localhost',
                'port' => 6379,
                'password' => getenv('REDIS_PASSWORD'),
                'database' => 0,
            ],
        ],
    ],
];
``` 

## Guzzle Config

Craft uses [Guzzle 6](http://docs.guzzlephp.org/en/latest/) whenever creating HTTP requests, such as:

- when checking for Craft updates
- when sending in a support request from the Craft Support widget
- when loading RSS feeds from the Feeds widget
- when working with assets on remote volumes, like Amazon S3

You can customize the config settings Guzzle uses when sending these requests by creating a `guzzle.php` file in your `config/` folder. The file should return an array, with your config overrides.

```php
<?php

return [
    'headers' => ['Foo' => 'Bar'],
    'query'   => ['testing' => '123'],
    'auth'    => ['username', 'password'],
    'proxy'   => 'tcp://localhost:80',
];
```

The options defined here will be passed into new `GuzzleHttp\Client` instances. See [Guzzle’s documentation](http://docs.guzzlephp.org/en/latest/) for a list of available options.

## Aliases

Some settings and functions in Craft support [Yii aliases](http://www.yiiframework.com/doc-2.0/guide-concept-aliases.html), which are basically placeholders for base file system paths and URLs. These include:

- Sites’ Base URL settings
- Volumes’ Base URL settings
- Local volumes’ File System Path settings
- The [resourceBasePath](https://docs.craftcms.com/api/v3/craft-config-generalconfig.html#$resourceBasePath-detail) and [resourceBaseUrl](https://docs.craftcms.com/api/v3/craft-config-generalconfig.html#$resourceBaseUrl-detail) config settings
- The [svg()](templating/functions.md#svg-svg-sanitize-) Twig function

The following aliases are available out of the box:

| Alias | Description
| ----- | -----------
| `@app` | The path to `vendor/craftcms/cms/src/`
| `@config` | The path to your `config/` folder
| `@contentMigrations` | The path to your `migrations/` folder
| `@craft` | The path to `vendor/craftcms/cms/src/`
| `@lib` | The path to `vendor/craftcms/cms/lib/`
| `@root` | The root project path (same as the `CRAFT_BASE_PATH` PHP constant)
| `@runtime` | The path to your `storage/runtime/` folder
| `@storage` | The path to your `storage/` folder
| `@templates` | The path to your `templates/` folder
| `@translations` | The path to your `translations/` folder
| `@vendor` | The path to your `vendor/` folder
| `@web` | The URL to the folder that contains the `index.php` file that was loaded for the request
| `@webroot` | The path to the folder that contains the `index.php` file that was loaded for the request

You can define additional custom aliases using the [aliases](https://docs.craftcms.com/api/v3/craft-config-generalconfig.html#$aliases-detail) config setting. For example, you may wish to create aliases that define the base URL and base path that your asset volumes will live in.

```php
'aliases' => [
    '@assetBaseUrl' => 'http://example.com/assets',
    '@assetBasePath' => '/path/to/web/assets',
],
```

With those in place, you could begin your asset volumes’ Base URL and File System Path settings with them, e.g. `@assetBaseUrl/user-photos` and `@assetBasePath/user-photos`.

If you’d like, you can set the alias values with environment variables, either from your `.env` file or somewhere in your environment’s configuration:

```
ASSET_BASE_URL=http://example.com/assets
ASSET_BASE_PATH=/path/to/web/assets
```

Then you can pull them into the alias definitions using [getenv()](http://php.net/manual/en/function.getenv.php):

```php
'aliases' => [
    '@assetBaseUrl' => getenv('ASSET_BASE_URL'),
    '@assetBasePath' => getenv('ASSET_BASE_PATH'),
],
```

## Overriding Volume Settings

If you would prefer to define volume settings with a config file, you can do that from `config/volumes.php`. The file should return an array whose keys map to your volume handles, and values are nested arrays that define the overridden setting values.

> {note} You must create your volumes within the Control Panel before Craft will start checking `config/volumes.php` for overrides.

```php
return [
    'siteAssets' => [
        'path' => getenv('ASSETS_BASE_PATH').'/site',
        'url' => getenv('ASSETS_BASE_URL').'/site',
    ],
    'companyLogos' => [
        'path' => getenv('ASSETS_BASE_PATH').'/logos',
        'url' => getenv('ASSETS_BASE_URL').'/logos',
    ],
];
```

## URL Rules

You can define custom [URL rules](http://www.yiiframework.com/doc-2.0/guide-runtime-routing.html#url-rules) in `config/routes.php`, which will get merged in with any routes you’ve defined on the Settings → Routes page in the Control Panel.

Craft supports a custom syntax for routing requests to a template, rather than a controller action:

```php
return [
    'blog/archive/<year:\d{4}>' => ['template' => 'blog/_archive'],
];
```

## Redactor Configs

You can customize the Redactor configurations that are available to Rich Text fields by saving them as `.json` files within your `config/redactor/` directory. The available config settings are listed in [Redactor’s documentation](https://imperavi.com/redactor/docs/settings/).

These `.json` files must contain **valid JSON**. That means:

- No comments
- All object properties (the config setting names) must be wrapped in double quotes
- All strings must use double quotes rather than single quotes

```javascript
// Bad:
{
  /* interesting comment */
  buttons: ['bold', 'italic']
}

// Good:
{
  "buttons": ["bold", "italic"]
}
```

## HTML Purifier Configs

You can customize the HTML Purifier configurations that are available to Rich Text fields by saving them as `.json` files within your `config/htmlpurifier/` directory. The available config settings are listed in [HTML Purifier’s documentation](http://htmlpurifier.org/live/configdoc/plain.html).

```json
{
  "HTML.AllowedCommentsRegexp": "p, div"
}
```

## Application Config

You can customize Craft’s entire [application configuration](http://www.yiiframework.com/doc-2.0/guide-structure-applications.html#application-configurations) from `config/app.php`. Any items returned by that array will get merged into the main application configuration array.

### Mailer Component

To override the `mailer` component config (which is responsible for sending emails), do this in `config/app.php`:

```php
<?php

return [
    'components' => [
        'mailer' => function() {
            // Get the stored email settings
            $settings = Craft::$app->systemSettings->getEmailSettings();

            // Override the transport adapter class
            $settings->transportType = craft\mailgun\MailgunAdapter::class;

            // Override the transport adapter settings
            $settings->transportSettings = [
                'domain' => 'foo.com',
                'apiKey' => 'key-xxxxxxxxxx',
            ];

            return craft\helpers\MailerHelper::createMailer($settings);
        },

        // ...
    ],

    // ...
];
```
