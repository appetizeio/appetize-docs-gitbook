# Delete app

{% api-method method="delete" host="https://APITOKEN@api.appetize.io" path="/v1/apps/:publicKey" %}
{% api-method-summary %}
Delete app
{% endapi-method-summary %}

{% api-method-description %}
Deletes an app. Your API token must be provisioned to the same account where the app was uploaded.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="publicKey" type="string" required=true %}
publicKey for the app
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

