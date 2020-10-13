# Usage summary

{% api-method method="get" host="https://APITOKEN@api.appetize.io" path="/v1/usageSummary" %}
{% api-method-summary %}
Get usage summary
{% endapi-method-summary %}

{% api-method-description %}
Gets usage summary of all sessions for your account, including number of sessions and session durations.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "hasMore": false, // indicates if results have been truncated
    "data": [{
        "month": "2016-06-01",
        "publicKey": "p7nww3n6ubq73r1nh9jtauqy8w",
        "numSessions": 325,
        "minutes" 162.5
    }, {
        "month": "2016-05-01",
        "publicKey": "p7nww3n6ubq73r1nh9jtauqy8w",
        "numSessions": 102,
        "minutes" 80.3
    }]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

