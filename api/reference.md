---
description: Our API is following REST guidelines and is HTTP based.
---

# Reference

## Authentification

Weglot uses API Keys to allow access to the API. You can register a new Weglot API Key at: [Register](https://dashboard.weglot.com/register).

Weglot expects for the API Key to be included in all API requests to the server in the URL as a parameter that looks like the following:

`https://api.weglot.com/endpoint?api_key=my_api_key` 

{% hint style="info" %}
 Make sure to replace `my_api_key` with your Weglot API key.
{% endhint %}

## Endpoints {#endpoints}

{% api-method method="post" host="https://api.weglot.com" path="/translate" %}
{% api-method-summary %}
Translate
{% endapi-method-summary %}

{% api-method-description %}
This endpoint retrieves all translations. It takes an array of sentences in an original languages in input and output the same array of sentences but translated in another languages.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter type="string" name="l\_from" required=true %}
ISO 639-1 code of the original language
{% endapi-method-parameter %}

{% api-method-parameter name="l\_to" type="string" required=true %}
ISO 639-1 code of the destination language
{% endapi-method-parameter %}

{% api-method-parameter name="" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter required=false name="" type="string" %}

{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```



```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://api.weglot.com" path="/status" %}
{% api-method-summary %}
Status
{% endapi-method-summary %}

{% api-method-description %}
This endpoint is used as check-alive. You can use it to check if Weglot API is up and running.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## Resources {#resources}

### BotType

Used to defined the source of a request.

| **Short-Name** | **Value** | **Description** |
| --- | --- | --- | --- | --- | --- | --- | --- |
| HUMAN | 0 | Sent from human action |
| OTHER | 1 | Sent from unknow source |
| GOOGLE | 2 | Sent from Google Bot |
| BING | 3 | Sent from Bing Bot |
| YAHOO | 4 | Sent from Yahoo Bot |
| BAIDU | 5 | Sent from Baidu Bot |
| YANDEX | 6 | Sent from Yandex Bot |

### WordType {#wordtype}

Used to defined how a sentence gonna be used.

| **Short-Name** | **Value** | **Description** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| OTHER | 0 | The word is none of the elements below \(deprecated\) |
| TEXT | 1 | Word is simple text \(used most of the time\) |
| VALUE | 2 | Word is an attribute value |
| PLACEHOLDER | 3 | Word is from a placeholder |
| META\_CONTENT | 4 | Word is from meta content header |
| IFRAME\_SRC | 5 | Word is an iframe source link |
| IMG\_SRC | 6 | Word is an image source link |
| IMG\_ALT | 7 | Word is an image alternative description |
| PDF\_HREF | 8 | Word is a PDF source link |

