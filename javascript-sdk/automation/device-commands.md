# Device commands

The client provides methods to configure the device and start a session, while the session provides methods for user interaction.

## Client

### startSession()

Starts a session with the requested app, device, operating system, and other launch options.

```typescript
const session = await client.startSession()
```

**Parameters**

| Name      | Type                  | Description                                                                                                     |
| --------- | --------------------- | --------------------------------------------------------------------------------------------------------------- |
| `config?` | `Record<string, any>` | A JSON object describing the [Configuration options](../configuration.md#configuration-options) for the device. |

### setConfig()

Update the configured app, device, operating system, or other launch options. See [Configuration](../configuration.md#configuration-options) for acceptable values.

_Note: This will end any active sessions._

```typescript
await client.setConfig(config)
```

### endSession()

Ends the active session or cancels any pending session requests.

```typescript
await client.endSession()
```

## **Session**

### adbShellCommand

Executes an `adb shell` command on the device (Android only)

{% code overflow="wrap" %}
```typescript
await session.adbShellCommand("am start -a android.intent.action.VIEW -d https://appetize.io/")
```
{% endcode %}

### allowInteractions()

Enables or disables all interactions on the device.

```typescript
await session.allowInteractions(false)
```

### biometry()

Simulate a matching fingerprint (Android 8+ only)

```typescript
await session.biometry({
    match: true/false
})
```

### end()

Ends the session

```typescript
await session.end()
```

### getUI()

{% hint style="warning" %}
**Experimental** \
The data structure of the response is subject to change
{% endhint %}

Returns an array of elements describing the current UI on the device.

```typescript
const ui = await session.getUI()

/*
[
  { type: 'app', appId: 'com.my.app', children: [...] },
  { type: 'app', appId: 'com.apple.springboard', children: [...] }
]
*/

```

### heartbeat()

Sends a heartbeat to the server, resetting the inactivity timer of the session

```typescript
await session.heartbeat()
```

### keypress()

Sends a single key press to the device.

```javascript
await session.keypress("a")
```

This can also be used to send hardware keys:

* `HOME`
* `VOLUME_UP` (Android)
* `VOLUME_DOWN` (Android)
* `ANDROID_KEYCODE_MENU` (Android)

### openUrl()

Opens a deep-link or web URL

```typescript
await session.openUrl("https://appetize.io")
```

### launchApp(appId)

{% hint style="warning" %}
This feature is currently under development and will be available soon.
{% endhint %}

Launches the specified application using the provided `appId`.&#x20;

{% hint style="info" %}
If the app is already running, it will be brought to the foreground instead of being relaunched. If the app was originally launched with params or a launchUrl, these will also be passed with this method.
{% endhint %}

```typescript
await session.launchApp(appId)
```

**Parameters**

| Name    | Type     | Description                                                                                                                                                                                                                                                                                                                   |
| ------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `appId` | `string` | <p><strong>Android:</strong> <br>The app's package name / appId (e.g., <code>com.example.app</code>) or <code>packageName/activityName</code>. If no activity name is specified, it defaults to the main launch activity. <br><strong>iOS:</strong> <br>The app's bundle identifier (e.g., <code>com.example.app</code>).</p> |

### restartApp()

Restarts the app

```typescript
await session.restartApp()
```

### reinstallApp()

Reinstalls the app

```typescript
await session.reinstallApp()
```

### rotate()

Rotates the device 90 degrees left or right

```typescript
await session.rotate('left')

await session.rotate('right')
```

### screenshot()

Takes a screenshot of the device and returns the data as a buffer.

```typescript
const { data, mimeType } = await session.screenshot()
```

Alternatively, it can return the data as a base64 encoded string

```javascript
const { data, mimeType } = await session.screenshot('base64')
```

### shake()

Shakes device (iOS only)

```typescript
await session.shake()
```

### toggleSoftKeyboard()

Toggles the soft keyboard (iOS only)

```typescript
await session.toggleSoftKeyboard()
```

### setLanguage()

Changes the current language.

```typescript
await session.setLanguage("fr")
```

{% hint style="warning" %}
If your app does not automatically handle language/locale changes, you would need to explicitly call [restartApp](device-commands.md#restartapp) for this to take effect.\
\
Some apps might also cache data in the previously used language. In these cases use [reinstallApp](device-commands.md#reinstallapp) to clear any previous cached data.
{% endhint %}

This&#x20;

### type()

Types the given text

```javascript
await session.type("hello")
```

{% hint style="warning" %}
Typing is limited to 1000 characters at a time to ensure optimal performance and prevent potential disruptions. For larger payloads, you can use multiple 'type' operations.
{% endhint %}

### waitForAnimations(options)

Waits until the there are no ongoing animations on the screen by waiting for the image to stabilize for at least 1 second.

```typescript
await session.waitForAnimations(options)
```

| Name                    | Type     | Description                                                                                                                                         |
| ----------------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| options.imageThreshold? | `number` | <p>The threshold for the amount of pixels (in %) that can change between frames before the image is considered to be stable.<br>(default 0.001)</p> |
| options.timeout?        | `number` | <p>The maximum amount of time (in ms) to wait for the image to stabilize.<br>(default 10s)</p>                                                      |
