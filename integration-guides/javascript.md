# Javascript

## Getting started

Let's include Weglot's client code into your site and get started with translations.

1. Go to your Weglot dashboard \([https://dashboard.weglot.com/](https://dashboard.weglot.com/)\) and get your API key in the "Project settings" menu \(e.g. `wg_1234567897e2ea993d291b571c2ec93b0`\)
2. Edit your HTML file, and right after the`<body>`tag, append the following code:

```markup
<script type="text/javascript" src="https://cdn.weglot.com/weglot.min.js"></script>
<script>
	Weglot.setup({
	  api_key: 'YOUR_API_KEY',
	  originalLanguage: 'en',
	  destinationLanguages : 'fr,es',
	 });
</script>
```

Make sure you replace `YOUR_API_KEY`with the API key you got in the step one.

You can now refresh your page. French and Spanish are now translation options for your website in English!

{% hint style="info" %}
The full list of language codes we support is available at [https://weglot.com/documentation/available-languages](https://weglot.com/documentation/available-languages)
{% endhint %}

## Initialization code

As you've seen in the "Getting started" section, Weglot gets initialized through this code:

```javascript
Weglot.setup(options)
```

Where `options` is a Javascript object with properties defined as follows. Only **`api_key`**, **`originalLanguage`** and **`destinationLanguages`** \(in bold\) are required.

| Property | Description | Default | Example |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **`api_key`** | Your Weglot API Key |  |  |
| **`originalLanguage`** | The ISO 639-1 code of the original language of your website |  | `"en"` |
| **`destinationLanguages`** | A comma-separated list of 2-letter codes of languages you wish to be able to translate your website to. |  | `"fr,es"` |
| `styleOpt` | A javascript object describing the default styling of the Weglot language switcher button |  | `{ fullname: true, withname: true, is_dropdown: true, classF: '' }` |
| `styleOpt["withname"]` | `true` to display a label text next to each language options. `false` otherwise | `true` |  |
| `styleOpt["fullname"]` | If `withname` is `true`, `true` to display the full name of the language.`false` to just show the 2-letter language code | `true` |  |
| `styleOpt["is_dropdown"]` | `true` to display the language selector as a dropdown. `false` to show it as a list | `true` |  |
| `styleOpt["classF"]` | A String. The extra CSS class to apply to the button elements. Add `wg-flags` to show flags \(by default they will be mat rectangles\). | `""` | `"wg-flags flag-3"` `"wg-flags"` |
| `autoSwitch` | `true` to automatically switch to the user's preferred language if available. `false` otherwise. | `false` |  |
| `exceptions` | A comma-separated list of CSS selectors of elements to exempt from translation | `""` | `"#not-this-id,.not-this-class"` |
| `dynamic` | A comma-separated list of CSS selectors of elements to watch for changes. If content changes dynamically inside one of the targeted elements, Weglot will translate it. | `""` | `".content-will-change-inside"` |
| `excludePaths` | A comma-separated list of paths to exclude from translations. The current path will be tested against Regex strings. | `""` | `"/blog/,/checkout/\d+"` |
| `waitTransition` | `true` to prevent content blinking when translating a new page. | `true` |  |
| `subDomain` | `true` to enable the [subdomain mode](javascript.md#subdomain-mode) | `false` |  |
| `hideSwitcher` | `true` to prevent Weglot from creating language switchers, false otherwise. Defaults to false. If you set it to true, it's your responsibility to use the [Client-side API](javascript.md#weglot-switchto-code) or [link hooks](javascript.md#link-hooks) to change languages on the page | `false` |  |
| `translateSearch` | `true` to translate search queries on the website, `false` otherwise.  | `false` |  |
| `searchsForms` | A comma-separated list of CSS selectors of search form elements to watch for. Useful only if `translateSearch` is `true`. The form has to send a `q` parameter for it to work | `""` |  |
| `switchers` | A Javascript Array of Objects representing several language switchers on the page | `[]` |  |
| `switchers[]["styleOpt"]` | A Javascript Object defined exactly like `styleOpt` |  |  |
| `switchers[]["target"]` | The CSS selector of the node that the switcher will be a child of |  | `".site-header__section--title"` |
| `switchers[]["sibling"]` | The CSS selector of the next sibling element of the switcher. `null` for the last element inside the target |  | `null` |

A full example could look like this:

```javascript
Weglot.setup({
  api_key: "wg_1234567897e2ea993d291b571c2ec93b0",
  originalLanguage: "en",
  destinationLanguages : "es,fr",
  styleOpt : { fullname: true , withname: true , is_dropdown: true , classF: "wg-flags flag-3" },
  exceptions: "#not-this-element,.not-this-class.p",
  excludePaths: "",
  dynamic: ".a-container-of-dynamic-content",
  autoSwitch: true,
  translateSearch: false,
  switchers: [
    {
      styleOpt:{
        fullname: true,
        withname: true,
        is_dropdown: true,
        classF: "wg-flags flag-3"
      },
      containerCss: "",
      target: ".site-header__section--title",
      sibling: null
    }
  ]
});
```

## Client-side API

### Weglot.getCurrentLang\(\)

{% tabs %}
{% tab title="Parameters" %}
None
{% endtab %}

{% tab title="Response" %}
String: the ISO 639-1 2-letter code of the current language on the page
{% endtab %}
{% endtabs %}

### Weglot.getLanguageName\(code\)

{% tabs %}
{% tab title="Parameters" %}
* code\(String\): the ISO 639-1 2-letter code of [a language supported by Weglot](https://weglot.com/documentation/available-languages)
{% endtab %}

{% tab title="Response" %}
String: the local name of the language, as defined by ISO 639-1

For example, calling `Weglot.getLanguageName("es")` returns `"Español"`
{% endtab %}
{% endtabs %}

### Weglot.switchTo\(code\)

{% tabs %}
{% tab title="Parameters" %}
* code\(String\): the ISO 639-1 2-letter code of a language you're supporting on your website

  code is either **originalLanguage** or one of the **destinationLanguages**
{% endtab %}

{% tab title="Response" %}
Nothing
{% endtab %}
{% endtabs %}

### Weglot.on\(eventName, callbackFunction\)

You can subscribe your own code to Weglot-specific events. When these events occur, the callback function you have defined will be called.

#### languageChanged

This is called right after a language has changed on the page

```javascript
Weglot.on("languageChanged", callbackFunction)
```

The callback function will be called with two optional arguments:

1. newLanguage \(String\): the 2-letter code of the language the page changed to
2. previousLanguage \(String\): the 2-letter code of the previous language of the page

Example:

```javascript
Weglot.on("languageChanged", function(newLang, prevLang) {
    console.log("The language on the page just changed to (code): " + newLang)
    console.log("The full name of the language is: " + Weglot.getLanguageName(newLang))
})
```

#### initialized

This is called right after the call to **Weglot.setup\(options\)** has been successful. The language switchers are now displayed and the nodes to translate are prepared. 

```javascript
Weglot.on("initialized", callbackFunction)
```

The callback function will be called with no argument.

{% hint style="info" %}
If you register your callback **after** Weglot has been initialized, this will have no effect.

To check whether Weglot is already initialized or not, you can read the boolean `Weglot.initialized`
{% endhint %}

### Weglot.off\(eventName, callbackFunction\)

With `Weglot.off`, you can unsubscribe the events you subscribed to with `Weglot.on`

{% tabs %}
{% tab title="Parameters" %}
eventName\(String\): **mandatory field**, the name of the event you want to unsubscribe from

callbackFunction\(Function\): **optional field**, if you'd like to target a specific function
{% endtab %}

{% tab title="Response" %}
**true** if one or more events have been unregistered

**false** otherwise
{% endtab %}
{% endtabs %}

### Weglot.setup\(options\)

Called to initialize Weglot. See [Initialization code](javascript.md#initialization-code)

## JS Library versions

Weglot's JS library comes in different versions. They are all stored in our CDN in a minified file.

Depending on the version you would like to use, you may want to change first line of code in the "Getting started" section. For example, to use the standard version of Weglot JS \(which is available at https://cdn.weglot.com/weglot.min.js\), the first line will be:

```markup
<script type="text/javascript" src="https://cdn.weglot.com/weglot.min.js"></script>
```

#### **Standard**

Available at _https://cdn.weglot.com/weglot.min.js_

Use this version when you're not installing Weglot on one of our supported platforms \(Shopify, Wix, Bigcommerce, etc.\)

The standard library works well with CMS such as Squarespace, Webflow, or any other website.

#### Shopify

Available at _https://cdn.weglot.com/weglot\_shopify.min.js_ 

This is the version used by Weglot's [Shopify app](https://apps.shopify.com/weglot). It's included automatically for you, hence we advise you to use our app directly for any Shopify store as some features come only from the app \(Checkout translation, drag-and-drop placement, etc.\)

This version adds a few Shopify-specific options and features.

#### **Bigcommerce**

Available at _https://cdn.weglot.com/weglot\_bigcommerce.min.js_

This is the version used by the [Bigcommerce app](https://www.bigcommerce.com/apps/weglot-translate/). It adds some convenience options that help setting the right customer language along the way, as well as support for cart drawers.

#### **Wix**

Available at _https://cdn.weglot.com/weglot\_wix.min.js_

This is the version any Wix user should use, as it loads the Weglot app once the Wix website has been initialised properly.

#### **Jimdo**

Available at _https://cdn.weglot.com/weglot\_jimdo.min.js_

This is the version any Jimdo user should use.

## Link hooks

By default, Weglot will show a language switcher on your page. Either on the bottom-right side or where it has been set through the `switchers` options. In some cases, you might want to not use Weglot's switcher at all and use menu entries from the CMS you're integrating in. You might also want to create your own switcher and not use Weglot's CSS.

When Weglot gets initialized, every link that matches one of these CSS selectors will be "hooked" to a `Weglot.switchTo` action automatically:

* `a[href='#Weglot-xx']`
* `a[href$='change-language.weglot.com/xx']`

... where `xx` is the ISO-639-1 code of the target language

When the links are "hooked", the original `href` attribute also gets removed, and the class `weglot-link` is added to them. The current language also has the class  `weglot-link--active`

### Example - Anchor

I want to use the native menu feature of my CMS. Let's say my original language is English, and I want to translate to French and Spanish.

My menu would have 3 entries, as follows:

| **Text** | **Link** |
| --- | --- | --- | --- |
| English | \#Weglot-en |
| Français | \#Weglot-fr |
| Español | \#Weglot-es |

I have now a "native" language switcher that works for all these languages. If I need to apply specific styling to the current language, I can target the `weglot-link--active`class.

### Example - Fake link

Sometimes, the CMS you will be using won't allow for anchor links in the menu \(e.g. Wix\). In this case, you can use fake links that will be replaced when Weglot initializes:

| **Text** | **Link** |
| --- | --- | --- |
| English | http://change-language.weglot.com/en |
| Français | http://change-language.weglot.com/fr |



## Subdomain mode

Passing `subDomain: true`on the initialization call allows Weglot to match the current subdomain to a target language. In this case, the preferred language is not stored over sessions, and the browser's preferred language \(`autoSwitch` option\) is ignored.

If your original language is English, and your destination languages are French and Spanish, this assumes the following setup:

| Hostname delivering the website | Language set by Weglot |
| --- | --- | --- | --- | --- | --- |
| www.mywebsite.com | English |
| mywebsite.com | English |
| fr.mywebsite.com | French |
| es.mywebsite.com | Spanish |
| something.mywebsite.com | English |

In this setup, **it's your responsibility** to set the right CNAME records so that `fr.mywebsite.com` and `es.mywebsite.com` point to the same server.

Any switcher or link hook set will keep working under this setup. They will redirect to the right hostname upon change.

## Example: create your own switcher

```javascript
function() {
    // CHANGE THIS SELECTOR to the element you want to add your custom switcher to.
    var myDiv = document.getElementById("myDiv");

    //Create array of options to be added
    var availableLanguages = [Weglot.options.originalLanguage].concat(Weglot.options.destinationLanguages.split(','))
    
    //Create and append select list
    var selectList = document.createElement("select");
    myDiv.appendChild(selectList);
    
    var currentLang = Weglot.getCurrentLang();
    
    //Create and append the options
    for (var i = 0; i < availableLanguages.length; i++) {
        var lang = availableLanguages[i];
        var option = document.createElement("option");
        option.value = lang;
        option.text = Weglot.getLanguageName(lang);
        if (lang === currentLang) {
            option.selected = "selected";        
        }
        selectList.appendChild(option);
    }
    
    selectList.onchange = function(){
        Weglot.switchTo(this.value);
    };
    
    Weglot.on("languageChanged", function(lang) {
        selectList.value = lang;
    })
}()
```

