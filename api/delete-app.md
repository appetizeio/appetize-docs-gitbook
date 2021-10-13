# Delete app

{% swagger baseUrl="https://APITOKEN@api.appetize.io" path="/v1/apps/:publicKey" method="delete" summary="Delete app" %}
{% swagger-description %}
Deletes an app. Your API token must be provisioned to the same account where the app was uploaded.
{% endswagger-description %}

{% swagger-parameter in="path" name="publicKey" type="string" %}
publicKey for the app
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```javascript
// N/A
```
{% endswagger-response %}
{% endswagger %}

