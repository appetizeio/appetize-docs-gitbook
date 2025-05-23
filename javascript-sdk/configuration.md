---
description: >-
  With Appetize's configuration options, users can easily switch between
  different device and operating system versions, languages, and many other
  options in order to customize their experience.
---

# Configuration

You can configure the client to change the device, OS version, app, and various other options. This will set the configuration for the embed before the session starts, either programmatically or by user interaction.

```javascript
await client.setConfig({
    device: 'iphone11pro',
    osVersion: '15.0'
})
```

Additionally, you can provide these when starting a session programmatically:

```javascript
const session = await client.startSession({
    device: 'iphone11pro',
    osVersion: '15.0'
})
```

{% hint style="info" %}
Initial values may also be provided in the embed URL. See [Query Params Reference](../platform/query-params-reference.md).
{% endhint %}

## Configuration Options

### buildId

`string`

The buildId (previously known as publicKey) of the Appetize app that you wish to run.

### device

`string`

The device to run on. [See Devices & OS Versions](../features/devices-and-os-versions.md).

### osVersion

`string`

The operating system version on which to run your app. e.g. 11.4, 12.2, 13.3, 14.0

_Note: We recommend leaving this blank so it will always use our latest default for the device._

### scale

`number | 'auto'`

Sets the scale of the device in the iframe.

If a number is provided it must be between 10 and 100. If `'auto'`, the device will scale up to fit inside the iframe.

### autoPlay

`boolean`

When true, starts streaming the app on device load. Default is `false`.

{% hint style="warning" %}
We recommend starting the session programmatically using `client.startSession()` instead as this could cause the session to start before the SDK is ready.
{% endhint %}

### adbShellCommand

`string`

&#x20;(Android only) Executes an `adb shell` command on the device.

### androidPackageManager

`boolean`

(Android only) Allows installation of additional APKs after app launch.

### appearance

`"dark" | "light"`

(iOS 13+ and Android 10+) Sets dark or light mode UI.

### audio

`boolean`

(Android Only) Enables audio playback on the device.

{% hint style="warning" %}
This feature is currently in Alpha and might not always work as expected.
{% endhint %}

### codec

`"h264" | "jpeg"`

Set the video codec used for the stream. Default is `h264` if the browser supports it, otherwise falls back to `jpeg`.

### debug

`boolean`

When true, the session will listen for debug logs and emit them as a `log` event.

### deviceColor

`"black" | "white"`

Sets the color of the device chrome.

### disableVirtualKeyboard

`boolean`

(Android only) When true, disabled the onscreen keyboard.

### enableAdb

`boolean`

(Android only) Sets up an SSH tunnel to allow ADB connections to the emulator. SSH command and info can be found by accessing the [adbConnection](api-reference/#adbconnection) property on the session.

For more information see [ADB tunnel](../features/advanced-features/android/adb-tunnel.md).

### grantPermissions

`boolean`

Automatically grant all required app permissions. [See Auto-grant permissions](../features/auto-grant-permissions.md).

### hidePasswords

`boolean`

(Android only) Hide password visibility when typing.

### iosKeyboard

`string`

Set the language for the iOS Keyboard. eg. `ja_JP@sw`. [See available values](https://pgssoft.github.io/AutoMate/Enums/SoftwareKeyboard.html).

### iosAutocorrect

`boolean`

Turn on Auto-Correction for iOS. Defaults to `true`.

### language

`string`

Sets the language of the device. Must be an [ISO 639-1 & BCP 47](https://stackoverflow.com/questions/7973023/what-is-the-list-of-supported-languages-locales-on-android) language code.

### launchApp

`boolean | string`

Indicates whether an app launches after installation and allows specifying which installed app to open.

**Possible values:**

* `false` - Apps install but do not launch.
* `true` or `undefined` – Default behavior
* `appId` - Launches the app with the specified [app Identifier](../platform/sharing-apps.md#app-identifier) (e.g., `com.android.chrome`).

### launchUrl

`string`

Specify a deep link to open when your app is launched.

### launchArgs

`string[]`

(iOS only) An array of strings to pass when launching your app.

### locale

`string`

(iOS only) Sets the locale of the device. Must be a locale ID e.g. `en_GB`, `fr_FR`.

### location

`number[]`

(iOS 12+, Android 10+) Sets location of the device in latitude and longitude. e.g.. \[`39.903924,116.391432]`

### noVideo

`boolean`

Sets whether the video feed is enabled.

### orientation

`"portrait" | "horizontal"`

Sets the orientation of the device

### platform

`'ios' | 'android'`

Sets the platform of the device.

### params

`object`

A JSON object that will be passed to your app on launch

### plistEdit

`Object`

Represents an object that allows additional key-value properties to be added to the app's plist, enabling customization or configuration of the app behavior during launch.

### proxy

`string`

Specify a proxy server to route network traffic. eg `http://example.com:8080`

For Appetize's built-in intercepting proxy, use `intercept`. Network logs are emitted from the session as a `network` event.

{% hint style="info" %}
Our current support is limited to HTTP Proxies. When your app makes HTTPS connections, the data remains encrypted despite the unencrypted connection to the proxy. The app sends a CONNECT request to the proxy for the destination HTTPS server, initiating an SSL handshake. The proxy acts as a TCP connection forwarder, ensuring end-to-end encryption for app data.
{% endhint %}

### record

`boolean`

Enables recording of all user actions that took place during the session. See [UI Automation](../features/ui-automation.md) for more information. Default is true.

### region

`us` | `eu`

Ensures that Appetize sessions are launched only from servers in a specific region.

{% hint style="warning" %}
It is best to avoid setting this property unless absolutely necessary. Our system automatically directs requests to the closest servers for optimal performance. Using this property could lead to longer queues in busy regions.
{% endhint %}

### screenOnly

`boolean`

If true, only show the screen and not the device chrome.

### showRotateButtons

`boolean`

Enables the display of rotate buttons next to the device. Requires `scale` to be set to `auto`.

### timezone

`string`

(Android only) Sets the timezone of the device. [See available values](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).

### endSessionRedirectUrl

`string`

Specifies the URL to redirect users to at the end of the session.&#x20;

### userInteractionDisabled

`boolean`

Sets whether user interaction is disabled.

### volume

`number`

Sets the audio playback level. The value ranges from `0` to `1`, defaults to `0.5`
