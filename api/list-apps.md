# List apps

{% swagger baseUrl="https://APITOKEN@api.appetize.io" path="/v1/apps/:publicKey" method="get" summary="Get a single app" %}
{% swagger-description %}
Retrieves information about a single app.
{% endswagger-description %}

{% swagger-parameter in="path" name="publicKey" type="string" %}
publicKey for the app
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```javascript
{
    "publicKey": "p7nww3n6ubq73r1nh9jtauqy8w",
    "created": "2016-02-10T17:46:14.089Z",
    "updated": "2016-02-10T17:46:14.089Z",
    "platform": "ios",
    "versionCode": 1
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://APITOKEN@api.appetize.io" path="/v1/apps" method="get" summary="Get all apps" %}
{% swagger-description %}
Retrieves information about all apps in the account, with associated metadata.
{% endswagger-description %}

{% swagger-parameter in="query" name="nextKey" type="string" %}
If results are truncated due to too many apps, response will include 

`hasMore: true`

 and 

`nextKey: "xyz"`

. Pass nextKey value as query parameter into GET request to retrieve the next batch of apps. 
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
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
{% endswagger-response %}
{% endswagger %}
