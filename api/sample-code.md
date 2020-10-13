# Sample code

The Appetize.io API is designed to be user friendly. Please see a few example API calls below. 

{% tabs %}
{% tab title="Curl" %}
```bash
curl --http1.1 https://APITOKEN@api.appetize.io/v1/apps \
-H 'Content-Type: application/json' \
-d '{"url":"FILE URL", "platform": "ios"}'
```
{% endtab %}

{% tab title="Node.js" %}
```javascript
// use the 'request' module from npm
var request = require('request');
request.post({
    url: 'https://APITOKEN@api.appetize.io/v1/apps',
    json: {
        url: 'FILE URL',
        platform: 'ios'
    }
}, function(err, response, body) {
    if (err) {
        // connection error
        console.log('Error', err);
    } else if (response.statusCode !== 200) {
        // API returned error
        console.log('API error', body);
    } else {
        // success
        console.log(body);
    }
});
```
{% endtab %}
{% endtabs %}



{% hint style="info" %}
Any questions at all? Please email us at [hello@appetize.io](mailto:hello@appetize.io).
{% endhint %}

