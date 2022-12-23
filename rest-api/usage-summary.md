# Usage summary

{% swagger baseUrl="https://APITOKEN@api.appetize.io" path="/v1/usageSummary" method="get" summary="Get usage summary" %}
{% swagger-description %}
Gets usage summary of all sessions for your account, including number of sessions and session durations.
{% endswagger-description %}

{% swagger-parameter in="query" name="nextKey" type="string" %}
If results are truncated, response will include 

`hasMore:true`

 and 

`nextKey: "xyz"`

. Pass nextKey value as query parameter into GET request to retrieve the next batch of results. 
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
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
{% endswagger-response %}
{% endswagger %}

