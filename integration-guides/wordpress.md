# WordPress

## Introduction

Weglot has built a powerful WordPress plugin that integrates in your WordPress website and make it multilingual in a few minutes.

What does Weglot plugin do exactly ?

1. It creates URL for each languages, like `/fr/about/` or `/es/about/` for instance
2. On these URL, it returns the translated content
3. It adds a language button on the page and the `hreflang` tags in the `<head>` section of your page for SEO.

## Getting started

To start, install [Weglot Translate](https://wordpress.org/plugins/weglot/) plugin directly from the directory.

In the settings page, configure the 3 mandatory settings :

* **API Key** : You get an API key in your account. If you don't have one, you can [create your account](https://dashboard.weglot.com/register-wordpress).
* **Original Language** : The original language of your WordPress website.
* **Destination Languages** : The languages you want your website to be translated into.

Save the settings and you are done. You will see the language button appear on your website.

## Plugin settings

#### Override CSS

You can add your own CSS rules to customize the language button.

Weglot automatically adds a button in your page, that is either a dropdown or a list.

{% tabs %}
{% tab title="Dropdown" %}
```markup
<aside data-wg-notranslate class="country-selector weglot-dropdown weglot-default weglot-invert">
    <input id="weglot_choice" type="checkbox" name="menu">
    <label for="weglot_choice" class="wgcurrent wg-li weglot-flags flag-0 en" data-code-language="en">
        <span>EN</span>
    </label>
    <ul>
        <li class="wg-li weglot-flags flag-0 fr" data-code-language="fr">
            <a data-wg-notranslate href="http://example.com/">FR</a>
        </li>
    </ul>
</aside>
```
{% endtab %}

{% tab title="List" %}
```markup
<aside data-wg-notranslate class="country-selector weglot-inline weglot-default weglot-invert">
    <input id="weglot_choice" type="checkbox" name="menu">
    <label for="weglot_choice" class="wgcurrent wg-li weglot-flags en" data-code-language="en">
        <span>English</span>
    </label>
    <ul>
        <li class="wg-li weglot-flags fr" data-code-language="fr">
            <a data-wg-notranslate href="http://example.com/fr/">Français</a>
        </li>
    </ul>
</aside>
```
{% endtab %}
{% endtabs %}

You can use these classes to ad your own rules. For example adding this in "Override CSS" : 

```css
.country-selector a {
    text-transform: uppercase;
}
```

will make the language name uppercase

#### Exclude URL

By default, all pages are translated. You can use this field to enter URL that you don't want to translate. This field matches regex.

For example, if you want to exclude all URL that contains `/blog/` , you can simply add "/blog/"  in the option.

Another example, if you want to only translate your homepage, meaning you want to exclude every URL except `/` , you would enter the following : `[^/]`

#### Exclude blocks

By default, everything is translated inside a page. But sometimes, you don't want to translate part of your page. For example all product descriptions or a customer review area.

You can add any CSS selector in the field "Exclude blocks" and it will add an attribute `data-wg-notranslate` on this HTML element. Everything inside this element won't be translated.

For example, if you enter this : `.product-description` , then your translated page will be : 

```markup
<h1 class="product-title">Mon super article</h1> <!--The title is being translated-->
<p class="product-description" data-wg-notranslate>My awesome article</p><!--The description is not being translated-->
```

## WordPress filters

Weglot plugin is using WordPress filters to extend default capabilities

### weglot\_words\_translate

{% hint style="info" %}
Since : 1.12
{% endhint %}

You can add words that are present in your HTML page but not translated. It's useful when a word is not being translated by Weglot because it's inside a Javascript for example. 

{% code-tabs %}
{% code-tabs-item title="functions.php" %}
```php
<?php
// File wp-content/themes/myTheme/functions.php​

add_filter('weglot_words_translate', 'words_translate');​
function words_translate($words){        
    $words[] = "Monday";       
    $words[] = "Tuesday";    
    $words[] = "Nice to meet you";           
    return $words;
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### weglot\_regex\_amp

{% hint style="info" %}
Since : 2.0

Default value : \(\[&\?/\]\)amp\(/\)?$
{% endhint %}

You can modify the regex that validates if a URL is an AMP page

{% code-tabs %}
{% code-tabs-item title="functions.php" %}
```php
<?php
// File wp-content/themes/myTheme/functions.php​

add_filter('weglot_regex_amp', 'regex_amp');​
function regex_amp($regex){        
    // Change regex $regex = 'other';      
    return $regex;
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### weglot\_is\_eligible\_url

{% hint style="info" %}
Since : 2.0
{% endhint %}

This hook allows you to influence whether or not you can translate a URL.

{% code-tabs %}
{% code-tabs-item title="functions.php" %}
```php
<?php
// File wp-content/themes/myTheme/functions.php​

add_filter('weglot_is_eligible_url', 'eligible_url');​
function eligible_url( $bool ){        
    if( get_post_type( get_the_ID() ) === 'premium-post' ) {
        return true;
    }

    return false;
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### weglot\_url\_auto\_redirect

{% hint style="info" %}
Since : 2.0
{% endhint %}

You can use this filter to change the automatic redirection URL

{% code-tabs %}
{% code-tabs-item title="functions.php" %}
```php
<?php
// File wp-content/themes/myTheme/functions.php​

add_filter('weglot_url_auto_redirect', 'auto_redirect');​
function eligible_url( $url ){        
    return "https://example.com";
}

```
{% endcode-tabs-item %}
{% endcode-tabs %}

### weglot\_active\_translation

{% hint style="info" %}
Since : 2.0
{% endhint %}

This filter allows you to enable or disable translation

{% code-tabs %}
{% code-tabs-item title="functions.php" %}
```php
<?php
// File wp-content/themes/myTheme/functions.php​

add_filter('weglot_active_translation', 'active_translation');​
function active_translation( $is_active ){     
    return false;
}

```
{% endcode-tabs-item %}
{% endcode-tabs %}

### weglot\_type\_treat\_page

{% hint style="info" %}
Since : 2.0
{% endhint %}

This filter allows you to add a translation type. By default we manage :

* html
* json

This filter must be combined with : weglot\_**%s**\_treat\_page

Example with **type = xml**

{% code-tabs %}
{% code-tabs-item title="functions.php" %}
```php
<?php
// File wp-content/themes/myTheme/functions.php​

add_filter('weglot_type_treat_page', 'type_treat_page');​
function type_treat_page( $type ){     
    return 'xml';
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="functions.php" %}
```php
<?php
// File wp-content/themes/myTheme/functions.php​

add_filter('weglot_xml_treat_page', 'xml_treat_page');​
function type_treat_page( $content ){     
    // You can modify the content as you wish
    return $content;
}

```
{% endcode-tabs-item %}
{% endcode-tabs %}

### weglot\_href\_lang

{% hint style="info" %}
Since : 2.0
{% endhint %}

This filter allows you to modify the HTML generation of href lang links

{% code-tabs %}
{% code-tabs-item title="functions.php" %}
```php
<?php
// File wp-content/themes/myTheme/functions.php​

add_filter('weglot_href_lang', 'htm_href_lang');​
function htm_href_lang( $content ){     
    // You can modify the content as you wish
    return $content;
}


```
{% endcode-tabs-item %}
{% endcode-tabs %}

### weglot\_button\_html

{% hint style="info" %}
Since 2.0
{% endhint %}

This filter allows you to modify the HTML generation of weglot selector

{% code-tabs %}
{% code-tabs-item title="functions.php" %}
```php
<?php
// File wp-content/themes/myTheme/functions.php​

add_filter('weglot_button_html', 'button_html');​
function button_html( $button_html ){     
    // You can modify the content as you wish
    return $button_html;
}

```
{% endcode-tabs-item %}
{% endcode-tabs %}

### weglot\_get\_dom\_checkers

{% hint style="info" %}
Since 2.0
{% endhint %}

This filter allows you to add a class to target an element of the DOM or attributes that are not translated

{% code-tabs %}
{% code-tabs-item title="functions.php" %}
```php
<?php
// File wp-content/themes/myTheme/functions.php​

add_filter('weglot_get_dom_checkers', 'get_dom_checkers');​
function get_dom_checkers( $dom_checkers ){     
    $dom_checkers[] = '\Namespace\ClassDomChecker';
    return $dom_checkers;
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### weglot\_exclude\_blocks

{% hint style="info" %}
Since 2.0
{% endhint %}

This filter allows you to add blocks to exclude that cannot be modified from the settings.

{% code-tabs %}
{% code-tabs-item title="functions.php" %}
```php
<?php
// File wp-content/themes/myTheme/functions.php​

add_filter('weglot_exclude_blocks', 'exclude_blocks');​
function exclude_blocks( $exclude_blocks ){     
    $exclude_blocks[] = '.description';
    return $exclude_blocks;
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### weglot\_exclude\_urls

{% hint style="info" %}
Since 2.0
{% endhint %}

This filter allows you to add urls to exclude that cannot be modified from the settings.

{% code-tabs %}
{% code-tabs-item title="functions.php" %}
```php
<?php
// File wp-content/themes/myTheme/functions.php​

add_filter('weglot_exclude_urls', 'exclude_urls');​
function exclude_blocks( $exclude_urls ){     
    $exclude_urls[] = '/my-new-url';
    return $exclude_urls;
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### weglot\_css\_custom\_inline

{% hint style="info" %}
Since 2.0
{% endhint %}

This filter allows you to add custom style by default without going through the settings.

{% code-tabs %}
{% code-tabs-item title="functions.php" %}
```php
<?php
// File wp-content/themes/myTheme/functions.php​

add_filter('weglot_css_custom_inline', 'css_custom_inline');​
function css_custom_inline( $css_custom ){     
    $css_custom .= '.country-selector { background-color: red; }'; 
    return $css_custom;
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Helper functions

Weglot plugin is exposing functions that can be called in your code.

To see the source code of all available functions, you can go to the file : **weglot-functions.php** \(Only with 2.0\)

#### getCurrentLanguage

{% hint style="danger" %}
**Warning : No longer available in version 2**
{% endhint %}

Retrieve the current language \(2 letters code\) of the page

```php
use Weglot\WeglotContext;
$current = WeglotContext::getCurrentLanguage() ;
```

#### getOriginalLanguage

{% hint style="danger" %}
**Warning : No longer available in version 2**
{% endhint %}

Retrieve the original language of the website, as saved in the weglot settings

```php
use Weglot\WeglotContext;
$original = WeglotContext::getOriginalLanguage();
```

#### getDestinationLanguage

{% hint style="danger" %}
**Warning : No longer available in version 2**
{% endhint %}

Retrieve an array of destination languages, as saved in the weglot settings

```php
use Weglot\WeglotContext;
$destinations = WeglotContext::getDestinationLanguage();
```

### weglot\_get\_service

{% hint style="info" %}
Since 2.0

**Params :** 

* $service \(string\) 

**Return :** Object
{% endhint %}

This function allows you to retrieve a "Service" class from the plugin

```php
<?php

$language_service = weglot_get_service( 'Language_Service_Weglot' );
```

### weglot\_get\_options

{% hint style="info" %}
Since 2.0

**Return :**  string
{% endhint %}

This function allows you to retrieve all options Weglot

```php
<?php

$options = weglot_get_options();
echo $options['original_language'];
```

### weglot\_get\_option

{% hint style="info" %}
Since 2.0

**Params :** 

* $key \(string\)

**Return :** string
{% endhint %}

This function allows you to retrieve a specific option Weglot

```php
<?php

$original_language = weglot_get_options( 'original_language' );
echo $original_language;
```

### weglot\_get\_current\_language

{% hint style="info" %}
Since 2.0

**Return :** string
{% endhint %}

Retrieves the current language of a page

```php
<?php

$current_language = weglot_get_current_language();
echo $current_language;
```

### weglot\_get\_destination\_language

{% hint style="info" %}
Since 2.0

**Return** : array
{% endhint %}

Retrieves destination languages option

```php
<?php

$destination_language = weglot_get_destination_language();
echo $destination_language[0];
```

### weglot\_get\_request\_url\_service

{% hint style="info" %}
Since 2.0

**Return :** Request\_Url\_Service\_Weglot
{% endhint %}

Retrieve Request URL Service Weglot

```php
<?php

$request_url_service = weglot_get_request_url_service();
```

### weglot\_get\_current\_and\_original\_language

{% hint style="info" %}
Since 2.0

**Return :** array
{% endhint %}

Recovers the original language and the common language

```php
<?php

$current_and_original = weglot_get_current_and_original_language();
echo $current_and_original['original'];
```

### weglot\_get\_languages\_available

{% hint style="info" %}
Since 2.0

**Return :**  array
{% endhint %}

Recovers languages available from Weglot

```php
<?php

$languages_available = weglot_get_languages_available();
echo $languages_available['fr']->getLocalName();
```

#### weglot\_get\_languages\_configured

{% hint style="info" %}
Since 2.0

**Params :**

* $type \(string\|null\) Default : null

**Return :** array
{% endhint %}

Get languages configured from options.

If type is null, you will retrieve an object. You can use "**code"** and retrieve only code language.

```php
<?php

$languages_configured = weglot_get_languages_configured();
echo $languages_configured[0]->getLocalName(); // Example : 'Français'

// Or
$languages_configured = weglot_get_languages_configured('code');
echo $languages_configured[0]; // Example : 'fr'
```

