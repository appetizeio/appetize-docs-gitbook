# API methods

{% api-method method="post" host="https://APITOKEN@api.appetize.io" path="/v1/apps" %}
{% api-method-summary %}
Create new app
{% endapi-method-summary %}

{% api-method-description %}
Creates new app, returns new publicKey.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="test2" type="string" required=false %}
test2
{% endapi-method-parameter %}

{% api-method-parameter name="test1" type="string" required=true %}
test1
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "publicKey": "p7nww3n6ubq73r1nh9jtauqy8w",
    "created": "2016-02-10T17:46:14.089Z",
    "updated": "2016-02-10T17:46:14.089Z",
    "platform": "ios",
    "versionCode": 1
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://APITOKEN@api.appetize.io" path="/v1/apps/:publicKey" %}
{% api-method-summary %}
Update existing app
{% endapi-method-summary %}

{% api-method-description %}
Updates existing app, maintains same publicKey.
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

{% api-method method="get" host="https://APITOKEN@api.appetize.io" path="/v1/apps/:publicKey" %}
{% api-method-summary %}
Get a single app
{% endapi-method-summary %}

{% api-method-description %}
Retrieves information about a single app.
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

{% api-method method="get" host="https://APITOKEN@api.appetize.io" path="/v1/apps" %}
{% api-method-summary %}
Get all apps
{% endapi-method-summary %}

{% api-method-description %}
Retrieves information about all apps in the account, with associated metadata. 
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

{% api-method method="delete" host="https://APITOKEN@api.appetize.io" path="/v1/apps/:publicKey" %}
{% api-method-summary %}
Delete app
{% endapi-method-summary %}

{% api-method-description %}
Deletes an app.
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

{% api-method method="get" host="https://APITOKEN@api.appetize.io" path="" %}
{% api-method-summary %}
Get usage summary
{% endapi-method-summary %}

{% api-method-description %}
Gets usage summary of all sessions for your account, including number of sessions and session durations.
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

