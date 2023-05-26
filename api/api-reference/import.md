# Import



{% swagger baseUrl="https://demo.getlynx.dev/api" method="post" path="/import" summary="Import links from file" %}
{% swagger-description %}
Bulk imports links from a CSV/JSON
{% endswagger-description %}

{% swagger-parameter in="body" name="service" required="true" %}
Source service to import from:&#x20;

shlink, yourls, lynx
{% endswagger-parameter %}

{% swagger-parameter in="body" name="file" type="File" required="true" %}
CSV or JSON File
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Links successfully imported" %}
```javascript
{
    "success": true,
    "message": "Imported 1000/1000 links!"
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid filetype/import fields" %}

{% endswagger-response %}

{% swagger-response status="406: Not Acceptable" description="Imports are not enabled in demo mode" %}

{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}
