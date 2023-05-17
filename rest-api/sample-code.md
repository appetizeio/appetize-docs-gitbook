# Sample code

The Appetize.io API is designed to be user friendly. Please see a few example API calls below.

### Create new app

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
const request = require('request');
const btoa = require('btoa');

const url = 'https://api.appetize.io/v1/apps';
const apiToken = 'APITOKEN';
const fileUrl = 'FILE URL';
const platform = 'ios';

const options = {
  url: url,
  json: {
    url: fileUrl,
    platform: platform
  },
  headers: {
    Authorization: 'Basic ' + btoa(apiToken + ':')
  }
};

request.post(options, function(err, response, body) {
  if (err) {
    // Connection error
    console.log('Error', err);
  } else if (response.statusCode !== 200) {
    // API returned error
    console.log('API error', body);
  } else {
    // Success
    console.log(body);
  }
});
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Any questions at all? Please email us at [hello@appetize.io](mailto:hello@appetize.io).
{% endhint %}
