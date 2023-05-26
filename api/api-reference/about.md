# About

{% swagger baseUrl="https://demo.getlynx.dev/api" method="get" path="/about" summary="Get About [Public]" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="About successfully returned" %}
```javascript
{
    "success": true,
    "result":{
        "domain":"https://demo.getlynx.dev",
        "demo":true,
        "umami": { // if enabled
            "site": "224d86da-1209-4b8b-ad98-b24d300efa55",
            "url": "https://analytics.umami.is/script.js",
    }
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://demo.getlynx.dev/api" method="get" path="/about" summary="Get About [Authenticated]" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" required="false" %}
Your API key
{% endswagger-parameter %}

{% swagger-parameter in="cookie" name="token" %}
Your JWT Session
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="About successfully returned" %}
```javascript
{
    "success": true,
    "result":{
        "domain":"https://demo.getlynx.dev",
        "demo":true,
        "version":"1.2.3",
        "accounts":1,
        "links":236,
        "umami": { // if enabled
            "site": "224d86da-1209-4b8b-ad98-b24d300efa55",
            "url": "https://analytics.umami.is/script.js",
    }
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}
