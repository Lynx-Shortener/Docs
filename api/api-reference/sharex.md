# ShareX

{% swagger baseUrl="https://demo.getlynx.dev/api" method="post" path="/sharex" summary="Create Link" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="secret" required="true" %}
API key
{% endswagger-parameter %}

{% swagger-parameter in="body" name="url" required="true" %}

{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Link successfully created" %}
```javascript
{
    "success": true,
    "url": "https://demo.getlynx.dev/website",
}
```
{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="Invalid Secret." %}

{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://demo.getlynx.dev/api" method="get" path="/sharex" summary="Get Config" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" required="false" %}
Your API key
{% endswagger-parameter %}

{% swagger-parameter in="cookie" name="token" %}
Your JWT Session
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Config successfully returned" %}
```javascript
{
    "success": true,
    "result": {
        "config": {
            "Version": "14.1.0",
            "Name": "Lynx",
            "DestinationType": "Lynx",
            "RequestMethod": "POST",
            "RequestURL": "https://demo.getlynx.dev/api/sharex",
            "Body": "MultipartFormData",
            "Arguments": {
                "secret": "uihJEIwC0jjGIF0BhZnY7xI90jN664La",
                "url": "{input}"
            },
            "URL": "{json:url}",
            "ErrorMessage": "{json:error}"
        }
    }
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}
