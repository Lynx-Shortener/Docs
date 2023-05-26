# Export



{% swagger baseUrl="https://demo.getlynx.dev/api" method="post" path="/export" summary="Export links to file" %}
{% swagger-description %}
Bulk export links to a CSV/JSON file
{% endswagger-description %}

{% swagger-parameter in="body" name="format" type="String" required="true" %}
csv or json
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Links successfully exported" %}
```javascript
{
    "success": true,
    "result": {
        "buffer": "BUFFER",
        "filename": "export-2adafb34-2e0b-45f8-8dab-21c64dcb28d5.json"
}
```
{% endswagger-response %}

{% swagger-response status="406: Not Acceptable" description="Exports are not enabled in demo mode" %}

{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}
