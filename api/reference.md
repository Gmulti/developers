---
description: Our API is following REST guidelines and is HTTP based.
---

# Reference

## Authentification

Weglot requires an API key to allow access to its endpoints. You can register and get a Weglot API Key at: [Register](https://dashboard.weglot.com/register).

The API key is to be included in all API requests to the server in the URL as the value of the `api_key` parameter, as follows:

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
This endpoint retrieves all translations. It takes an array of sentences in an original language in input and outputs the same array of sentences but translated in another language.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Content-Type" type="string" required=false %}
application/json
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="api\_key" type="string" required=true %}
Your Weglot API Key
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}

{% api-method-body-parameters %}
{% api-method-parameter type="string" name="l\_from" required=true %}
ISO 639-1 code of the original language
{% endapi-method-parameter %}

{% api-method-parameter name="l\_to" type="string" required=true %}
ISO 639-1 code of the destination language
{% endapi-method-parameter %}

{% api-method-parameter name="words" type="array" required=true %}
Sentences in original language
{% endapi-method-parameter %}

{% api-method-parameter name="words\[t\]" type="integer" required=true %}
Type of the word based on WordType resource
{% endapi-method-parameter %}

{% api-method-parameter name="words\[w\]" type="string" required=true %}
Sentence to translate
{% endapi-method-parameter %}

{% api-method-parameter name="bot" required=false type="integer" %}
Link to user agent based on BotType resource
{% endapi-method-parameter %}

{% api-method-parameter name="request\_url" type="string" required=true %}
URL where the request come from
{% endapi-method-parameter %}

{% api-method-parameter name="title" type="string" %}
Title of the page where these sentences come from
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Usual return with two basic sentences:
{% endapi-method-response-example-description %}

```javascript
{  
   "l_from":"en",
   "l_to":"fr",
   "title":"My awesome page",
   "request_url":"https:\/\/www.website.com\/",
   "bot":0,
   "from_words":[  
      "This is a blue car",
      "This is a black car"
   ],
   "to_words":[  
      "C'est une voiture bleue",
      "C'est une voiture noire"
   ]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

You can find [WordType](reference.md#wordtype) and [BotType](reference.md#bottype) resources at the end of this document.

{% api-method method="get" host="https://api.weglot.com" path="/status" %}
{% api-method-summary %}
Status
{% endapi-method-summary %}

{% api-method-description %}
This endpoint is used as a health check. You can use it to check if the Weglot API is up and running.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
[]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
No content is returned by this endpoint, you will only get a 200 status code if the service is up and running.
{% endhint %}

{% hint style="danger" %}
This is only a health check endpoint, don't spam it.
{% endhint %}

## Resources {#resources}

### BotType

Used to defined the source of a request.

| **Short-Name** | **Value** | **Description** |
| --- | --- | --- | --- | --- | --- | --- | --- |
| HUMAN | 0 | Sent from human action |
| OTHER | 1 | Sent from unknown source |
| GOOGLE | 2 | Sent from Google Bot |
| BING | 3 | Sent from Bing Bot |
| YAHOO | 4 | Sent from Yahoo Bot |
| BAIDU | 5 | Sent from Baidu Bot |
| YANDEX | 6 | Sent from Yandex Bot |

### WordType {#wordtype}

Used to provide context over where the text we wish to translate comes from. Any general text node is of WordType **1**.

| **Short name** | **Value** | **Description** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| OTHER | 0 | None of the elements below \(deprecated\) |
| TEXT | 1 | General text \(used most of the time\) |
| VALUE | 2 | The value of an input tag's`value`attribute |
| PLACEHOLDER | 3 | The value of an input tag's `placeholder`attribute |
| META\_CONTENT | 4 | The value of a `meta` tags' `content` attribute |
| IFRAME\_SRC | 5 | The `src` link to a page used in an `iframe` |
| IMG\_SRC | 6 | The `src`value of an `img`tag |
| IMG\_ALT | 7 | The `alt` value of an `img`tag |
| PDF\_HREF | 8 | A URL pointing to a PDF document |



