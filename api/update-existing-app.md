# Update existing app

{% api-method method="post" host="https://APITOKEN@api.appetize.io" path="/v1/apps/:publicKey" %}
{% api-method-summary %}
Update existing app
{% endapi-method-summary %}

{% api-method-description %}
Updates existing app, maintains same publicKey. Your API token must be provisioned to the same account where the app was uploaded. To replace a previously set field, use a value of `null`. The POST body must be a JSON object.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="publicKey" type="string" required=true %}
publicKey for the app
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-body-parameters %}
{% api-method-parameter name="url" type="string" required=false %}
A publicly accessible link to your .zip, .tar.gz, or .apk file.
{% endapi-method-parameter %}

{% api-method-parameter name="platform" type="string" required=false %}
ios or android, defaults to the current app platform.
{% endapi-method-parameter %}

{% api-method-parameter name="fileType" type="string" required=false %}
The type of file that the url points to. Must be zip, tar.gz, or apk. Default is zip for ios, apk for android.
{% endapi-method-parameter %}

{% api-method-parameter name="note" type="string" required=false %}
A note for your own purposes, will appear on your management dashboard.
{% endapi-method-parameter %}

{% api-method-parameter name="timeout" type="number" required=false %}
The number of seconds to wait until automatically ending the session due to user inactivity. Must be 30, 60, 90, 120, 180, 300 or 600, default is 120.
{% endapi-method-parameter %}

{% api-method-parameter name="disabled" type="boolean" required=false %}
Disables streaming for this app.
{% endapi-method-parameter %}

{% api-method-parameter name="disableHome" type="boolean" required=false %}
Disables the home button on the iOS simulator when available.
{% endapi-method-parameter %}

{% api-method-parameter name="useLastFrame" type="boolean" required=false %}
Show the last image on the screen in the simulator after session ends.
{% endapi-method-parameter %}

{% api-method-parameter name="buttonText" type="string" required=false %}
Customize the message prompting the user to start the session, default is "Tap to play".
{% endapi-method-parameter %}

{% api-method-parameter name="postSessionButtonText" type="string" required=false %}
Customize the message prompting the user to restart the session, default is "Tap to play".
{% endapi-method-parameter %}

{% api-method-parameter name="launchUrl" type="string" required=false %}
Specify a deep link to bring your users to a specific location when your app is launched.
{% endapi-method-parameter %}

{% api-method-parameter name="appPermissions" type="object" required=false %}
Values for each field determine who can perform the specified action.  
  
**Values**  
"authenticated" - must be authenticated into your account  
"public" - anybody with app's publicKey \(26-character unguessable string\)  
null - resets to default  
  
**Fields**  
`run`: run your app  
`networkProxy`: specify a network proxy when running app  
`networkIntercept`: use Appetize.io's intercepting proxy when running the app  
`debugLog`: view your app's NSLog or Logcat output  
`adbConnect`: debug your app by connecting ADB to the hosted emulator  
`androidPackageManager`: allow the installation of additional APK's while your app is running
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
    "versionCode": 2 // increments with each update
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

