---
description: Seamless integration of Weglot into your Laravel project.
---

# Laravel

[![WeglotSlack](https://camo.githubusercontent.com/457f046a2d43d9c73260618a0cb55c6dd85f9a6c/68747470733a2f2f7765676c6f742d636f6d6d756e6974792e6e6f772e73682f62616467652e737667)](https://weglot-community.now.sh/) [![Latest Stable Version](https://camo.githubusercontent.com/98d5306946b3dd71eebf627860fde409bcbd541b/68747470733a2f2f706f7365722e707567782e6f72672f7765676c6f742f7472616e736c6174652d6c61726176656c2f762f737461626c65)](https://packagist.org/packages/weglot/translate-laravel) [![Maintainability](https://camo.githubusercontent.com/0a934cfa0737e06449410247ccb358efe00dd4ee/68747470733a2f2f6170692e636f6465636c696d6174652e636f6d2f76312f6261646765732f35373434333261326663623637323331613130392f6d61696e7461696e6162696c697479)](https://codeclimate.com/github/weglot/translate-laravel/maintainability) [![License](https://camo.githubusercontent.com/0e4d4702ba04f313eb00acd66b8e59f0c55d48c7/68747470733a2f2f706f7365722e707567782e6f72672f7765676c6f742f7472616e736c6174652d6c61726176656c2f6c6963656e7365)](https://packagist.org/packages/weglot/translate-laravel)

### Requirements

* PHP version 5.5 and later
* Weglot API Key, starting at [free level](https://dashboard.weglot.com/register)

### Installation

You can install the library via [Composer](https://getcomposer.org/). Run the following command:

```bash
composer require weglot/translate-laravel
```

To use the library, use Composer's [autoload](https://getcomposer.org/doc/01-basic-usage.md#autoloading):

```php
require_once __DIR__. '/vendor/autoload.php';
```

### Getting Started

#### Package Register

**Laravel 5**

Add Weglot package in the `config/app.php`:

```php
return [
    // ...

    'providers' => [
        // ... Other packages ...
        Weglot\Translate\TranslateServiceProvider::class
    ],

    // ...
];
```

#### Configuration

As usual for Laravel packages, you can publish configuration files by doing:

```bash
php artisan vendor:publish --provider="Weglot\Translate\TranslateServiceProvider" --tag="config"
```

You'll find the configuration file in `config/weglot-translate.php`:

```php
<?php

return [
    'api_key' => env('WG_API_KEY'),
    'original_language' => config('app.locale', 'en'),
    'destination_languages' => [
        'fr'
    ],
    'exclude_blocks' => ['.site-name'],
    'cache' => false,

    'laravel' => [
        'controller_namespace' => 'App\Http\Controllers',
        'routes_web' => 'routes/web.php'
    ]
];
```

This is an example of configuration, enter your own API key, your original language and destination languages that you want.

* `api_key` : is your personal API key. You can get an API Key by signing up on [Weglot](https://weglot.com/).
* `original_language` : original language is the language of your website before translation.
* `destination_languages` : are the languages that you want your website to be translated into.
* `cache` : if you wanna use cache or not. It's not a required field and set as false by default. Look at [Caching part](https://github.com/weglot/translate-laravel#caching) for more details.
* `laravel.controller_namespace` : Used internaly when rewriting routes, change it if your Laravel namespace isn't `App` or your controllers are moved.
* `laravel.routes_web` : Used internaly when rewriting routes, refer to the file where you have all your web routes.

There is also a non-required parameters `exclude_blocks` where you can list all blocks you don't want to be translated. On this example, you can see that all blocks with the `site-name` class won't be translated.

#### Caching

We implemented usage of `Cache` Facade for our package.

If you wanna use cache, just put the `cache` parameter to true in this package configuration. It will plug onto the Laravel cache behavior.

#### Optional - Hreflang links

Hreflang links are a way to describe your website and to tell webcrawlers \(such as search engines\) if this page is available in other languages. More details on Google post about hreflang: [support.google.com/webmasters/answer/189077](https://support.google.com/webmasters/answer/189077)

You can add them through the helper function: `weglotHrefLangRender`

Just put the function at the end of your `<head>` tag:

```markup
<html>
    <head>
        ...

        {{ weglotHrefLangRender() }}
    </head>
```

#### Optional - Language button

You can add a language button with the helper function: `weglotButtonRender`

Two layouts exists:

```markup
<!-- first layout -->
{{ weglotButtonRender(1) }}

<!-- second layout -->
{{ weglotButtonRender(2) }}
```

### Examples

You'll find a short README with details about example on each repository:

* [weglot/weglot-laravel-example-l5](https://github.com/weglot/weglot-laravel-example-l5)

### About

`translate-laravel` is guided and supported by the Weglot Developer Team.

`translate-laravel` is maintained and funded by Weglot SAS. The names and logos for `translate-laravel` are trademarks of Weglot SAS.

### License

[The MIT License \(MIT\)](https://github.com/weglot/translate-laravel/blob/develop/LICENSE.txt)

