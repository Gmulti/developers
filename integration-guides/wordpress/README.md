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
<aside data-wg-notranslate class="wg-default wg-drop country-selector closed weglot-selector" onclick="openClose(this);" >
   <div data-wg-notranslate class="wgcurrent wg-li wg-flags flag-3 en"><a href="#" onclick="return false;" >English</a></div>
   <ul>
      <li class="wg-li wg-flags flag-3 zh"><a data-wg-notranslate href="http://yourwebsite.com/zh/">中文 (简体)</a></li>
      <li class="wg-li wg-flags flag-3 fr"><a data-wg-notranslate href="http://yourwebsite.com/fr/">Français</a></li>
      <li class="wg-li wg-flags flag-3 es"><a data-wg-notranslate href="http://yourwebsite.com/es/">Español</a></li>
      <li class="wg-li wg-flags flag-3 el"><a data-wg-notranslate href="http://yourwebsite.com/el/">Ελληνικά</a></li>
   </ul>
</aside>
```
{% endtab %}

{% tab title="List" %}
```markup
<aside data-wg-notranslate class="wg-default wg-list country-selector closed weglot-selector" onclick="openClose(this);" >
   <li data-wg-notranslate class="wgcurrent wg-li wg-flags flag-3 en"><a href="#" onclick="return false;" >English</a></li>
   <li class="wg-li wg-flags flag-3 ar"><a data-wg-notranslate href="http://wptest.weglot.com/ar/">‏العربية‏</a></li>
   <li class="wg-li wg-flags flag-3 zh"><a data-wg-notranslate href="http://wptest.weglot.com/zh/">中文 (简体)</a></li>
   <li class="wg-li wg-flags flag-3 fr"><a data-wg-notranslate href="http://wptest.weglot.com/fr/">Français</a></li>
   <li class="wg-li wg-flags flag-3 es"><a data-wg-notranslate href="http://wptest.weglot.com/es/">Español</a></li>
   <li class="wg-li wg-flags flag-3 el"><a data-wg-notranslate href="http://wptest.weglot.com/el/">Ελληνικά</a></li>
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



