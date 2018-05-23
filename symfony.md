---
description: Seamless integration of Weglot into your Symfony project.
---

# Symfony

[![WeglotSlack](https://camo.githubusercontent.com/457f046a2d43d9c73260618a0cb55c6dd85f9a6c/68747470733a2f2f7765676c6f742d636f6d6d756e6974792e6e6f772e73682f62616467652e737667)](https://weglot-community.now.sh/) [![Latest Stable Version](https://camo.githubusercontent.com/767618fa6cfb228d7053b2dbeb7be4513a846e23/68747470733a2f2f706f7365722e707567782e6f72672f7765676c6f742f7472616e736c6174652d62756e646c652f762f737461626c65)](https://packagist.org/packages/weglot/translate-bundle) [![Maintainability](https://camo.githubusercontent.com/1a65f54fd56ea33a3426ab08b43d2c234c0c9872/68747470733a2f2f6170692e636f6465636c696d6174652e636f6d2f76312f6261646765732f62313738356431653932323538363966336461302f6d61696e7461696e6162696c697479)](https://codeclimate.com/github/weglot/translate-bundle/maintainability) [![License](https://camo.githubusercontent.com/caf896c9ab5fb404800617b2e99017d19ff413ec/68747470733a2f2f706f7365722e707567782e6f72672f7765676c6f742f7472616e736c6174652d62756e646c652f6c6963656e7365)](https://packagist.org/packages/weglot/translate-bundle)

### Requirements

* PHP version 5.5 and later
* Weglot API Key, starting at [free level](https://dashboard.weglot.com/register)

### Installation

You can install the library via [Composer](https://getcomposer.org/). Run the following command:

```bash
composer require weglot/translate-bundle
```

When you require the bundle with `symfony/flex` \(available for `symfony/symfony:^4.0`\) it should ask you if you wanna execute a recipe, tell `yes`. Like that it will make bundle registration in `config/bundles.php` & default config creation in `config/packages/weglot_translate.yml`.

To use the library, use Composer's [autoload](https://getcomposer.org/doc/01-basic-usage.md#autoloading):

```php
require_once __DIR__. '/vendor/autoload.php';
```

### Getting Started

#### Bundle Register

**Symfony 4**

Add Weglot bundle in the `config/bundles.php`:

```php
return [
    Symfony\Bundle\FrameworkBundle\FrameworkBundle::class => ['all' => true],
    // ... Other bundles ...
    Weglot\TranslateBundle\WeglotTranslateBundle::class => ['all' => true],
];
```

**Symfony 3 & 2**

Add Weglot bundle to `app/AppKernel.php` file:

```php
$bundles = array(
    new Symfony\Bundle\FrameworkBundle\FrameworkBundle(),
    // ... Other bundles ...
    new Weglot\TranslateBundle\WeglotTranslateBundle(),
);
```

#### Configuration

For Symfony 4, create configuration file under `config/packages/weglot_translate.yml` and add following content. For Symfony 3 & 2, add following content to your `app/config/config.yml`.

```yaml
weglot_translate:
    api_key: 'YOUR_WEGLOT_API_KEY'
    original_language : 'en'
    cache: false
    destination_languages:
        - 'fr'
        - 'de'
```

This is an example of configuration, enter your own API key, your original language and destination languages that you want.

* `api_key` : is your personal API key. You can get an API Key by signing up on [Weglot](https://weglot.com/).
* `original_language` : original language is the language of your website before translation.
* `destination_languages` : are the languages that you want your website to be translated into.
* `cache` : if you wanna use cache or not. It's not a required field and set as false by default. Look at [Caching part](https://github.com/weglot/translate-bundle#caching) for more details.

There is also a non-required parameters `exclude_blocks` where you can list all blocks you don't want to be translated. For example, if I've a block with class "site-name", you've to do as following:

```yaml
    exclude_blocks:
        - .site-name
```

#### Caching

We implemented usage of `weglot.translations` service for both Symfony 4 and Symfony 3 \(`symfony/cache` bundle was released with Symfony 3, so no compatibility for Symfony 2\).

If you wanna use cache, just add `cache: true` to this bundle configuration. It will use a file-based cache through Symfony [`FilesystemAdapter`](https://symfony.com/doc/current/components/cache/adapters/filesystem_adapter.html)

To clear the cache, you just have to use our custom command:

```bash
$ php bin/console weglot:cache:clear
```

#### Optional - Hreflang links

Hreflang links are a way to describe your website and to tell webcrawlers \(such as search engines\) if this page is available in other languages. More details on Google post about hreflang: [support.google.com/webmasters/answer/189077](https://support.google.com/webmasters/answer/189077)

You can add them through the Twig function: `weglot_hreflang_render`

Just put the function at the end of your `<head>` tag:

```markup
<html>
    <head>
        ...

        {{ weglot_hreflang_render() }}
    </head>
```

#### Optional - Language button

You can add a language button if you're using Twig with function: `weglot_translate_render`

Two layouts exists:

```markup
<!-- first layout -->
{{ weglot_translate_render(1) }}

<!-- second layout -->
{{ weglot_translate_render(2) }}
```

### Examples

You'll find a short README with details about example on each repository

* Symfony 4: [weglot/translate-bundle-example-sf4](https://github.com/weglot/translate-bundle-example-sf4)
* Symfony 3: [weglot/translate-bundle-example-sf3](https://github.com/weglot/translate-bundle-example-sf3)
* Symfony 2: [weglot/translate-bundle-example-sf2](https://github.com/weglot/translate-bundle-example-sf2)

### About

`translate-bundle` is guided and supported by the Weglot Developer Team.

`translate-bundle` is maintained and funded by Weglot SAS. The names and logos for `translate-bundle` are trademarks of Weglot SAS.

### License

[The MIT License \(MIT\)](https://github.com/weglot/translate-bundle/blob/develop/LICENSE.txt)

