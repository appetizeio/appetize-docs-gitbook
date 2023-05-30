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

### restartApp()

Restarts the app

```typescript
await session.restartApp()
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

### setLanguage()

Changes the current language and restarts the app

```typescript
await session.setLanguage("fr")
```

### type()

Types the given text

```javascript
await session.type("hello")
```

###
