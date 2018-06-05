---
description: JS client's API
---

# API

All the following entries are attributes of the **Weglot** window variable. Hence, **getCurrentLang\(\)** can be called from the window context by calling **Weglot.getCurrentLang\(\)**

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

`Weglot.on("languageChanged", callbackFunction)`

The callback function will be called with two optional arguments:

1. newLanguage \(String\): the 2-letter code of the language the page changed to
2. previousLanguage \(String\): the 2-letter code of the previous language of the page

#### initialized

This is called right after the call to **Weglot.setup\(options\)** has been successful. The language switchers are now displayed and the nodes to translate are prepared. 

`Weglot.on("initialized", callbackFunction)`

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

Called to initialize Weglot. See [Initialization code](./#initialization-code)

