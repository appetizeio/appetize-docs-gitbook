# Create new app

{% swagger baseUrl="https://APITOKEN@api.appetize.io" path="/v1/apps" method="post" summary="Create new app" expanded="true" %}
{% swagger-description %}
Creates new app, returns new publicKey. The POST body must be a JSON object.
{% endswagger-description %}

{% swagger-parameter in="body" name="url" type="string" %}
A publicly accessible link to your .zip, .tar.gz, or .apk file.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="platform" type="string" %}
ios or android
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fileType" type="string" %}
The type of file that the url points to. Must be zip, tar.gz, or apk. Default is zip for ios, apk for android.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="note" type="string" %}
A note for your own purposes, will appear on your management dashboard.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timeout" type="number" %}
The number of seconds to wait until automatically ending the session due to user inactivity. Must be 30, 60, 90, 120, 180, 300, 600, 1800, 3600 or 7200, default is 120.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="disabled" type="boolean" %}
Disables streaming for this app.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="disableHome" type="boolean" %}
Disables the home button on the iOS simulator when available.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="useLastFrame" type="boolean" %}
Show the last image on the screen in the simulator after session ends.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="buttonText" type="string" %}
Customize the message prompting the user to start the session, default is "Tap to play".
{% endswagger-parameter %}

{% swagger-parameter in="body" name="postSessionButtonText" type="string" %}
Customize the message prompting the user to restart the session, default is "Tap to play".
{% endswagger-parameter %}

{% swagger-parameter in="body" name="launchUrl" type="string" %}
Specify a deep link to bring your users to a specific location when your app is launched.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="appPermissions" type="object" %}
Values for each field determine who can perform the specified action.

\




\




**Values**

\


"authenticated" - must be authenticated into your account

\


"public" - anybody with app's publicKey (26-character unguessable string)

\


null - resets to default

\




\




**Fields**

\




`run`

: run your app

\




`networkProxy`

: specify a network proxy when running app

\




`networkIntercept`

: use Appetize.io's intercepting proxy when running the app

\




`debugLog`

: view your app's NSLog or Logcat output

\




`adbConnect`

: debug your app by connecting ADB to the hosted emulator

\




`androidPackageManager`

: allow the installation of additional APK's while your app is running
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```javascript
{
    "publicKey": "p7nww3n6ubq73r1nh9jtauqy8w",
    "created": "2016-02-10T17:46:14.089Z",
    "updated": "2016-02-10T17:46:14.089Z",
    "platform": "ios",
    "versionCode": 1 // increments with each update
}
```
{% endswagger-response %}
{% endswagger %}
