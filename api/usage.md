# Using the API

## Get your API keys

Your API requests are authenticated using API keys. Most endpoints support API keys, but some do not, such as account management endpoints, for security purposes.

You can generate an API key from your Settings page at any time. These do not expire unless replaced with a new one.

## Make your first request

To make your first request, send an authenticated request to the /api/auth/me endpoint. This will return information about your currently logged in account.

{% swagger baseUrl="https://demo.getlynx.dev/api" method="get" path="/auth/me" summary="Get Account" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" required="false" %}
Your API key
{% endswagger-parameter %}

{% swagger-parameter in="cookie" name="token" %}
Your JWT Session
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Account successfully returned" %}
```javascript
{
    "success": true,
    "result":{
        "id":"be8881ce-af01-433b-a675-fe02e8a48a88",
        "username":"demo",
        "email":"demo@example.com",
        "role":"standard",
        "secret":"uihJEIwC0jjGIF0BhZnY7xI90jN664La",
        "totp": false,
    }
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Invalid secret" %}

{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}
