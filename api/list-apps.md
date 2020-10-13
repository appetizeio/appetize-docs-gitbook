# List apps

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
{% api-method-parameter name="publicKey" type="string" required=true %}
publicKey for the app
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
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

{% api-method method="get" host="https://APITOKEN@api.appetize.io" path="/v1/apps" %}
{% api-method-summary %}
Get all apps
{% endapi-method-summary %}

{% api-method-description %}
Retrieves information about all apps in the account, with associated metadata.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="nextKey" type="string" required=false %}
If results are truncated due to too many apps, response will include `hasMore: true` and `nextKey: "xyz"`. Pass nextKey value as query parameter into GET request to retrieve the next batch of apps. 
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "hasMore": true, // if results have been truncated
    "nextKey": "xyz", // query parameter for next batch of results
    "data": [{
        "publicKey": "p7nww3n6ubq73r1nh9jtauqy8w",
        "created": "2016-02-10T17:46:14.089Z",
        "updated": "2016-02-10T17:46:14.089Z",
        "platform": "ios",
        "versionCode": 1
    }, {
        "publicKey": "48g0593mgxut2fz57yw2hdjd24",
        "created": "2016-02-10T17:44:38.613Z",
        "updated": "2016-02-10T17:44:38.613Z",
        "platform": "ios",
        "versionCode": 3
    }]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

