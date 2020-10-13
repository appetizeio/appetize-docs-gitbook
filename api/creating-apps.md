# Creating apps

Send an HTTP POST request to

```text
https://APITOKEN@api.appetize.io/v1/apps
```

Replace `APITOKEN` with your API token. The POST body must be a JSON object with the fields:

**Required Fields**

* `url`: \(string\) a publicly accessible link to your `.zip`, `.tar.gz`, or `.apk` file
* `platform`: \(string\) `ios` or `android`

**Optional Fields**

* `fileType`: \(string\) the type of file that the url points to. Must be `zip`, `tar.gz`, or `apk`. Default is `zip` for ios, `apk` for android.
* `timeout`: \(number\) the number of seconds to wait until automatically ending the session due to user inactivity. Must be `30`, `60`, `90`, `120`, `180`, `300` or `600`, default is `120`.
* `disableHome`: \(boolean\) disables the home button on the iOS simulator.
* `disabled`: \(boolean\) disables streaming for this app.
* `useLastFrame`: \(boolean\) show the last image on the screen in the simulator after session ends.
* `buttonText`: \(string\) customize the message prompting the user to start the session, default is "Tap to play".
* `postSessionButtonText`: \(string\) customize the message prompting the user to restart the session, default is "Tap to play".
* `launchUrl`: \(string\) specify a deep link to bring your users to a specific location when your app is launched.
* `appPermissions`: \(object\) a JSON object. Values can be "authenticated", "public", or null to reset to default. Keys can be:
  * `run`: run your app
  * `networkProxy`: specify a network proxy when running app
  * `networkIntercept`: use Appetize.io's intercepting proxy when running the app
  * `debugLog`: view your app's NSLog or Logcat output
  * `adbConnect`: debug your app by connecting ADB to the hosted emulator
  * `androidPackageManager`: allow the installation of additional APK's while your app is running
* `note`: \(string\) a note for your own purposes, will appear on your management dashboard.

**Example request object**

```text

{
    "url": "http://www.example.com/my_app.zip",
    "platform": "ios",
    "timeout": 300,
    "note": "CI build #42"
}
```

