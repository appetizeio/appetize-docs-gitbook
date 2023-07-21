# List apps

{% swagger baseUrl="https://APITOKEN@api.appetize.io" path="/v1/apps/:publicKey" method="get" summary="Get a Single App" %}
{% swagger-description %}
Retrieves information about a single app.
{% endswagger-description %}

{% swagger-parameter in="path" name="publicKey" type="string" required="true" %}
publicKey for the app
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "publicKey": "p7nww3n6ubq73r1nh9jtauqy8w",
    "created": "2016-02-10T17:46:14.089Z",
    "updated": "2016-02-10T17:46:14.089Z",
    "platform": "ios",
    "bundle": "com.example.app",
    "name": "example",
    "appDisplayName": "Example App",
    "appVersionCode": "1",
    "appVersionName": "1.0.0",
    "versionCode": 1,
    "iconUrl": "https://example.com/app.png",
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://APITOKEN@api.appetize.io" path="/v1/apps" method="get" summary="Get All Apps  - Paginated" %}
{% swagger-description %}
Retrieves information about all apps in the account, with associated metadata.&#x20;

_Recommended_ _approach for retrieving all apps._
{% endswagger-description %}

{% swagger-parameter in="query" name="nextKey" type="string" required="false" %}
If results are truncated due to too many apps, response will include

`hasMore: true`

and

`nextKey: "xyz"`

. Pass nextKey value as query parameter into GET request to retrieve the next batch of apps.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "hasMore": true, // if results have been truncated
    "nextKey": "xyz", // query parameter for next batch of results
    "data": [{
        "publicKey": "p7nww3n6ubq73r1nh9jtauqy8w",
        "created": "2016-02-10T17:46:14.089Z",
        "updated": "2016-02-10T17:46:14.089Z",
        "platform": "ios",
        "bundle": "com.example.app",
        "name": "example",
        "appDisplayName": "Example App",
        "appVersionCode": "1",
        "appVersionName": "1.0.0",
        "versionCode": 1,
        "iconUrl": "https://example.com/app.png",
    }, {
        "publicKey": "48g0593mgxut2fz57yw2hdjd24",
        "created": "2016-02-10T17:44:38.613Z",
        "updated": "2016-02-10T17:44:38.613Z",
        "platform": "ios",
        "bundle": "com.example.app2",
        "name": "example",
        "appDisplayName": "Example App",
        "appVersionCode": "1",
        "appVersionName": "1.0.0",
        "versionCode": 3,
        "iconUrl": "https://example.com/app2.png",
    }]
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/v1/apps/all" baseUrl="https://APITOKEN@api.appetize.io" summary="Get All Apps - Not Paginated" %}
{% swagger-description %}
Retrieves information about all apps in the account, with associated metadata.&#x20;

_**NOTE**: No pagination is performed so this query might be slow. It is recommended to use the paginated version of this query if possible._
{% endswagger-description %}

{% swagger-response status="200: OK" description="" %}
```json
{
    "data": [{
        "publicKey": "p7nww3n6ubq73r1nh9jtauqy8w",
        "created": "2016-02-10T17:46:14.089Z",
        "updated": "2016-02-10T17:46:14.089Z",
        "platform": "ios",
        "bundle": "com.example.app",
        "name": "example",
        "appDisplayName": "Example App",
        "appVersionCode": "1",
        "appVersionName": "1.0.0",
        "versionCode": 1,
        "iconUrl": "https://example.com/app.png",
    }, {
        "publicKey": "48g0593mgxut2fz57yw2hdjd24",
        "created": "2016-02-10T17:44:38.613Z",
        "updated": "2016-02-10T17:44:38.613Z",
        "platform": "ios",
        "bundle": "com.example.app2",
        "name": "example",
        "appDisplayName": "Example App",
        "appVersionCode": "1",
        "appVersionName": "1.0.0",
        "versionCode": 3,
        "iconUrl": "https://example.com/app2.png",
    }]
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/v1/apps/:publicKey" baseUrl="https://APITOKEN@api.appetize.io" summary="Get an App Group" %}
{% swagger-description %}
Retrieves information about an app group and all the apps associated with it.
{% endswagger-description %}

{% swagger-parameter in="path" name="publicKey" type="string" required="true" %}
publicKey for the app group (starts with 

`ag_`

)
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```json
{
    "publicKey": "ag_{publicKey}",
    "updated": "2023-07-21T12:50:21.492Z",
    "name": "App Group Name",
    "created": "2023-05-05T08:35:39.967Z",
    "createdBy": "user@appetize.io",
    "apps": [
        "{app 1 publicKey}",
        "{app 2 publicKey}"
    ]
}
```
{% endswagger-response %}
{% endswagger %}
