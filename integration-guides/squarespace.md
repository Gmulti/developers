---
description: How to Integrate Weglot on your Squarespace website
---

# Squarespace

## Using Weglot JS

Follow the [Getting started guide](javascript.md#getting-started). You can also use [link hooks](javascript.md#link-hooks) to create Squarespace native menu entries to switch language.

## Using Weglot Translation Network \(private feature\)

Weglot Translation Network allows you to translate your Squarespace website with unique features. Try our demo site at [https://weglot-sqspace.com](https://weglot-sqspace.com) and its Weglot-translated counterparts at [https://fr.weglot-sqspace.com](https://fr.weglot-sqspace.com/) and [https://es.weglot-sqspace.com](https://es.weglot-sqspace.com/)

Features include:

* One clean URL for each translated page
* First-class SEO, following all Google SEO guidelines
* Social media sharing of your translated pages
* No content-flash : the initial render of the website is correct!
* All other Weglot features: initial machine translation, a simple dashboard where you can edit all your translations, etc.
* ... No extra cost included! Your plan will still follow pricing defined at [https://weglot.com/pricing](https://weglot.com/pricing)

### Step 1: Get in touch with us

Write an email to support@weglot.com, mentioning that you want to use Weglot Translation Network for your Squarespace website. Also mention:

* The URL to your current Squarespace website \(eg.: mywebsite.com\)
* The extra languages that you want to start with \(eg.: French, Spanish, Arabic\)

### Step 2: We get back to you

We will get back to you with clear instructions on some DNS records to create.

* One CNAME record to verify your ownership of the domain and issue an SSL certificate on your behalf
* One CNAME record for each language that you wish to add

### Step 3: Enjoy!

Once you have confirmed that the records were properly created, we will add your website to Weglot's Translation Network. It will take approximately 1 hour in business hours for us to get back to you with a confirmation that your websites are ready. Your websites:

* fr.mywebsite.com
* es.mywebsite.com

are now ready!

### Step 4 \(optional\): Include the Weglot switcher on your Squarespace website

In the "Inject code" of the advanced settings, include the following code:

```markup
<script type="text/javascript" src="https://cdn.weglot.com/weglot.min.js"></script>
<script>
    Weglot.setup({
      api_key: 'your_api_key',
      originalLanguage: 'en',
      destinationLanguages : 'fr,es',
      subDomain: true
     });
</script>
```

This will add a language switcher on the bottom right side of your website. See the [Javascript](javascript.md#initialization-code) documentation for more options.

For a "native" menu, you can also add 3 menu entries in the Squarespace menu\(s\) of your choice:

* "English" - menu entry of type "Link", that links to `#Weglot-en`
* "Français" - menu entry of type "Link", that links to `#Weglot-fr`
* "Español" - menu entry of type "Link", that links to `#Weglot-es`

Weglot will remove its default switcher create dynamic links automatically for you. [Read more here](javascript.md#link-hooks).

