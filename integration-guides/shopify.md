# Shopify

## Tutorials

### Multi-domain setup

{% hint style="info" %}
This feature is using the [Subdomain mode](javascript.md#subdomain-mode) of the Javascript library. Feel free to read more about it there
{% endhint %}

In this example, we're gonna assume that your original language is English \(en\), and that you want to provide dedicated subdomains to your two other languages, French \(fr\) and Spanish \(es\). The primary domain of your Shopify store is www.mystore.com

#### Step 1: Adding new subdomains to your Shopify store

We now need to add **fr.mystore.com** and **es.mystore.com** to the domains connected to your store. Please follow [this guide from Shopify](https://help.shopify.com/manual/domains/connecting-existing-domains/setting-up-your-domain#connect-a-subdomain) to do so.

#### Step 2: Enabling the subdomain mode

In your Shopify Admin, go to the  **Themes** menu, then select **Actions &gt; Edit code** for your current theme.

Find the files `weglot_switcher.liquid` and `weglot_hreftags.liquid`

In `weglot_switcher.liquid`, add the option `subDomain: true` to the call to `Weglot.setup()`. The file will now look like this:

{% code-tabs %}
{% code-tabs-item title="weglot\_switcher.liquid" %}
```markup
<!--Start Weglot Script-->
<script type="text/javascript" src="https://cdn.weglot.com/weglot_shopify.min.js"></script>
<script>
    Weglot.setup({
      live: true,
      api_key: "your_api_key",
      originalLanguage: "en",
      destinationLanguages : "ar,fr",
      styleOpt : { fullname : true , withname : true , is_dropdown : true , classF : "wg-flags flag-3 " },
      exceptions: "",
      excludePaths: "",
      dynamic: ".slideshow__heading",
      autoSwitch: false,
      translateSearch: false,
      subDomain : true,
      switchers: [{"styleOpt":{"fullname":true,"withname":true,"is_dropdown":true,"classF":"wg-flags flag-3"},"containerCss":"","target":".site-header__section--title","sibling":null}]
     });
</script>
<!--End Weglot Script-->
<style id="weglot-custom-css"></style>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

In `weglot_hreftags.liquid`, replace the line `{% assign sub_domains = false %}` by `{% assign sub_domains = true %}` The file will now look like this:

{% code-tabs %}
{% code-tabs-item title="weglot\_hreftags.liquid" %}
```text
{% comment %} Variables set by Weglot's preferences panel {% endcomment %}
{% assign original_language = "en" %}
{% assign destination_languages = "es,fr" | split: ',' %}
{% assign proxy_prefix = "/a/l/" %}
{% assign sub_domains = true %}

{% comment %} Can be common code {% endcomment %}
{% assign protocol_part = canonical_url | split: '://' | first | append: '://' %}
{% assign full_domain = canonical_url | split: '://' | last | split: '/' | first %}
{% assign path = canonical_url | remove_first: protocol_part | remove_first: full_domain %}

{% if 1==2 %}{% else %}
<link rel="alternate" hreflang="{{ original_language }}" href="{{ canonical_url }}">
{% if sub_domains %}
{% assign main_domain = full_domain  %}
  {% for language in destination_languages %}
    <link rel="alternate" hreflang="{{ language }}" href="{{ protocol_part }}{{ language }}.{{ main_domain }}{{ path }}">
  {% endfor %}
{% else %}
  {% for language in destination_languages %}
    <link rel="alternate" hreflang="{{ language }}" href="{{ protocol_part }}{{ full_domain }}{{ proxy_prefix }}{{ language }}{{ path }}">
  {% endfor %}
{% endif %}
{% endif %}
<link rel="stylesheet" href="https://cdn.weglot.com/weglot_shopify.min.css" type="text/css" media="all">
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Send language data to Klaviyo

#### Through a signup form

This guide will add an extra property called `lang` to each user that signs up through a Klaviyo form on your website. It's then up to you to create segments on Klaviyo to send them emails of different languages.

First, locate the HTML ID of the Klaviyo signup form on your page \(Usually `email_subscribe`\). The selector to that form is then `#email_subscribe`

Include the following snippet in your HTML code. Make sure you include it **after** both `Weglot` and `KlaviyoSubscribe` are included. Make sure you replace `#email_subscribe` with the actual selector to the form.

```markup
<script>
function() {
  var attachLangToKlaviyo = function(lang) {
    KlaviyoSubscribe.attachToForms('#email_subscribe', {
      hide_form_on_success: true,
      extra_properties: {
        $lang: lang
      }
    })  
  }
  attachLangToKlaviyo(Weglot.getCurrentLang())
  Weglot.on('languageChanged', attachLangToKlaviyo)
}()
</script>
```

