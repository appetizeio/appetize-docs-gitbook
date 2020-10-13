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
{% api-method-query-parameters %}
{% api-method-parameter name="nextKey" type="string" required=false %}
If results are truncated, response will include `hasMore:true` and `nextKey: "xyz"`. Pass nextKey value as query parameter into GET request to retrieve the next batch of results. 
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



