---
description: >-
  With Appetize's configuration options, users can easily switch between
  different device and operating system versions, languages, and many other
  options in order to customize their experience
---

# Configuration

You can configure the client to change the device, OS version, currently loaded app (publicKey), and various other options.

```javascript
await client.config({
    device: 'iphone11pro',
    osVersion: '15.0'
})
```

Additionally, you can provide these when requesting a session:

```javascript
const session = await client.startSession({
    device: 'iphone11pro',
    osVersion: '15.0'
})
```

## Configuration Options

### device

`string`

The device to run on. [See Devices & OS Versions](../features/devices-and-os-versions.md).

### osVersion

`string`

The operating system version on which to run your app. e.g. 11.4, 12.2, 13.3, 14.0

_Note: We recommend leaving this blank so it will always use our latest default for the device_

### scale

`number`

Sets the scale of the device. Value must be between 10 and 100.

### orientation

`"portrait" | "horizontal"`

Sets the orientation of the device

### centered

`"vertical" | "horizontal" | "both"`

Centers the device within the embed

### deviceColor

`"black" | "white"`

Sets the color of the device chrome

### screenOnly

`boolean`

If true, only show the screen and not the device chrome

### language

`string`

Sets the language of the device. Must be an [ISO 639-1 & BCP 47](https://stackoverflow.com/questions/7973023/what-is-the-list-of-supported-languages-locales-on-android) language code.

### locale

`string`

(iOS only) Sets the locale of the device. Must be a locale ID e.g. `en_GB`, `fr_FR`

### iosKeyboard

`string`

Set the language for the iOS Keyboard. eg. `ja_JP@sw`. [See available values](https://pgssoft.github.io/AutoMate/Enums/SoftwareKeyboard.html)

### disableVirtualKeyboard

`boolean`

(Android only) When true, disabled the onscreen keyboard

### location

`number[]`

(iOS 12+, Android 10+) Sets location of the device in latitude and longitude. eg. \[`39.903924,116.391432]`

### timezone

`string`

(Android only) Sets the timezone of the device. [See available values](https://en.wikipedia.org/wiki/List\_of\_tz\_database\_time\_zones)

### grantPermissions

`boolean`

(Android only) Automatically grant all required app permissions

### hidePasswords

`boolean`

(Android only) Hide password visibility when typing

### launchUrl

`string`

Specify a deep link to open when your app is launched

### launchArgs

`string[]`

(iOS only) An array of strings to pass when launching your app

### debug

`boolean`

When true, the session will listen for debug logs and emit them as a `log` event.

### proxy

`string`

Specify a proxy server to route network traffic. eg `http://example.com:8080`

For Appetize's built-in intercepting proxy, use `intercept`. Network logs are emitted from the session as a `network` event.

{% hint style="info" %}
Our current support is limited to HTTP Proxies. When your app makes HTTPS connections, the data remains encrypted despite the unencrypted connection to the proxy. The app sends a CONNECT request to the proxy for the destination HTTPS server, initiating an SSL handshake. The proxy acts as a TCP connection forwarder, ensuring end-to-end encryption for app data.
{% endhint %}

### record

`boolean`

Enables recording of all user actions that took place during the session. See [UI Automation](../features/ui-automation.md) for more information.

### enableAdb

`boolean`

(Android only) Sets up an SSH tunnel to allow ADB connections to the emulator. SSH command and info can be found by quering [getAdbInfo](api-reference.md#getadbinfo) on the session.

### androidPackageManager

`boolean`

(Android only) Allows installation of additional APKs after app launch

### appearance

`"dark" | "light"`

(iOS 13+ and Android 10+) Sets dark or light mode UI

### params

`object`

A JSON object that will be passed to your app on launch

### publicKey

`string`

The publicKey of the app that you wish to run
