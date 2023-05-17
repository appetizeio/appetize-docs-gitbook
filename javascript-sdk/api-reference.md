# API reference

## getClient()

Get an instance of the Appetize client.

```javascript
const client = await window.appetize.getClient('#my_iframe')
```

**Parameters**

| Name     | Type     | Description                                             |
| -------- | -------- | ------------------------------------------------------- |
| selector | `string` | A query selector string pointing to the embedded iframe |

## Client

### on() <a href="#on-client" id="on-client"></a>

Listens for an event of the given name

```typescript
client.on(event, data => {
   console.log(data)
})
```

| Event               | Data Type                                             | Description                                                                                                                                                                                                                                                                                                                                |
| ------------------- | ----------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <h4>queue</h4>      | `{ type: 'account' \| 'session' , position: number }` | <p>Your position in queue for the device.<br><br>If <code>type</code> is <code>account</code> you have reached the maximum amount of concurrent sessions for your account and are in queue for the next available slot.<br><br>If <code>type</code> is <code>session</code>, you are in a queue to wait for the next available device.</p> |
| <h4>error</h4>      | `string`                                              | An error has occurred                                                                                                                                                                                                                                                                                                                      |
| <h4>deviceInfo</h4> | `Record<string, any>`                                 | <p>Information about the current device, such as type, orientation, and screen dimensions.<br><br>It also contains rendered dimensions of the device within the embed.</p>                                                                                                                                                                 |
| <h4>session</h4>    | `Session`                                             | A new session has started, either by `client.startSession()` or the user clicking "Tap to Play" on the device                                                                                                                                                                                                                              |

### startSession()

Starts a session with the requested app, device, operating system, and other launch options.

```typescript
const session = await client.startSession()
```

**Parameters**

| Name      | Type                  | Description                                                                                                  |
| --------- | --------------------- | ------------------------------------------------------------------------------------------------------------ |
| `config?` | `Record<string, any>` | A JSON object describing the [Configuration options](configuration.md#configuration-options) for the device. |

#### config()

Update the configured app, device, operating system, or other launch options.

_Note: This will end any active sessions._

```typescript
await client.config(config)
```

**Parameters**

| Name     | Type                  | Description                                                                                                  |
| -------- | --------------------- | ------------------------------------------------------------------------------------------------------------ |
| `config` | `Record<string, any>` | A JSON object describing the [Configuration options](configuration.md#configuration-options) for the device. |

### loadApp

Changes the loaded Appetize app of the iframe. This will restart your session, and you can also pass in `config` as well.

## **Session**

### on() <a href="#on-session" id="on-session"></a>

Listens for an event of the given name

```typescript
session.on(event, data => {
   console.log(data)
})
```

| Event                       | Data Type                                                                                                                | Description                                                                                                                                                                                                                                                                                                                                    |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <h4>log</h4>                | `{ message: string }`                                                                                                    | <p>Debug log from the device<br><br>Requires <a href="configuration.md#debug">debug</a> to be set to <code>true</code></p>                                                                                                                                                                                                                     |
| <h4>network</h4>            | `Record<string, any>`                                                                                                    | <p>Intercepted network request or responses.</p><p>Requires <a href="configuration.md#proxy">proxy</a> to be set to <code>intercept</code></p>                                                                                                                                                                                                 |
| <h4>error</h4>              | `string`                                                                                                                 | An error has occurred on the session                                                                                                                                                                                                                                                                                                           |
| <h4>action</h4>             | `Record<string, any>`                                                                                                    | An action has been recorded                                                                                                                                                                                                                                                                                                                    |
| <h4>interaction</h4>        | `Record<string, any>`                                                                                                    | Session received interaction from the user                                                                                                                                                                                                                                                                                                     |
| <h4>inactivityWarning</h4>  | `{ secondsRemaining: number }`                                                                                           | <p>Session is about to timeout due to inactivity.</p><p>Any user interaction or a <a href="api-reference.md#heartbeat">heartbeat</a> will reset the timeout.</p>                                                                                                                                                                               |
| <h4>orientationChanged</h4> | `'portrait' \| 'landscape'`                                                                                              | The device has changed orientation                                                                                                                                                                                                                                                                                                             |
| <h4>video</h4>              | <p><code>{</code><br><code>buffer: Uint8Array, width: number, height: number, codec: string</code><br><code>}</code></p> | <p>Video frames of the current session.<br><br>When codec is <code>h264</code>, the buffer is a raw frame of the stream. These frames can be muxed (using something like <a href="https://github.com/samirkumardas/jmuxer">jmuxer</a>) to turn it into a video format.<br><br>When codec is <code>jpeg</code> the buffers are jpeg images.</p> |
| <h4>audio</h4>              | <p><code>{</code><br><code>buffer: Uint8Array, codec: 'aac'</code><br><code>}</code></p>                                 | <p>Audio frames of the current session.<br><br>Like <code>h264</code> with the <code>video</code> event, these can be muxed as well.</p>                                                                                                                                                                                                       |

### end()

Ends the session

```typescript
await session.end()
```

### rotate()

Rotates the device 90 degrees

```typescript
await session.rotate('right')
```

**Parameters**

| Name      | Type                | Description             |
| --------- | ------------------- | ----------------------- |
| direction | `"left" \| "right"` | The direction to rotate |

### screenshot()

Takes a screenshot of the device and returns the data

```typescript
const { data, mimeType } = await session.screenshot(format)
```

**Parameters**

| Name   | Type                   | Description                                 |
| ------ | ---------------------- | ------------------------------------------- |
| format | `"buffer" \| "base64"` | The format of the screenshot data to return |

### heartbeat()

Sends a heartbeat to the server, resetting the inactivity timer

```typescript
await session.heartbeat()
```

### tap()

Taps on the screen at the given position

```typescript
await session.tap({ x: 100, y: 100 })
```

**Parameters**

| Name          | Type                      | Description                                                     |
| ------------- | ------------------------- | --------------------------------------------------------------- |
| `coordinates` | `{ x: number, y: number}` | The coordinates of the position to tap, relative to the screen. |

### type()

Types the given text on the device

```typescript
await session.type("hello")
```

**Parameters**

| Name   | Type     | Description  |
| ------ | -------- | ------------ |
| `text` | `string` | Text to type |

### keypress()

Sends a single key press to the device

```typescript
await session.keypress("a")
```

**Parameters**

| Name      | Type                  | Description                                                                                                                                                                                                                                             |
| --------- | --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `key`     | `string`              | <p>Key to send to the device ('a', 'b', etc.)<br><br>Also takes special values for hardware keys:<br><br><code>HOME</code><br><code>VOLUME_UP</code> (android only)<br><code>VOLUME_DOWN</code> (android only)<br><code>ANDROID_KEYCODE_MENU</code></p> |
| `options` | `{ shift?: boolean }` |                                                                                                                                                                                                                                                         |

### setLanguage()

Changes the current language and restarts the app

```typescript
await session.setLanguage("fr")
```

**Parameters**

| Name       | Type     | Description   |
| ---------- | -------- | ------------- |
| `language` | `string` | Language code |

### setLocation()

Sets the simulated location of the device.

```typescript
await setLocation(-33.924434, 18.418391)
```

#### Parameters

| Name        | Type   | Description                                                                                                                                                                                                          |
| ----------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `latitude`  | number | Decimal number between -90 and 90, representing the degrees of north or south of the Equator. Negative numbers indicate south of the Equator, and positive numbers indicate north of the Equator.                    |
| `longitude` | number | Decimal number between -180 and 180, representing the degrees of east or west of the Prime Meridian. Negative numbers indicate west of the Prime Meridian, and positive numbers indicate east of the Prime Meridian. |

### openUrl()

Opens a deep-link or web URL

```typescript
await session.openUrl("https://appetize.io")
```

**Parameters**

| Name  | Type     | Description |
| ----- | -------- | ----------- |
| `url` | `string` | The URL     |

### shake()

Shakes device (iOS only)

```typescript
await session.shake()
```

### biometry()

Simulate a matching fingerprint (Android 8+ only)

```typescript
await session.biometry({
    match: true/false
})
```

### allowInteractions()

Enables or disables all interactions on the device. Default is true.

```typescript
await session.allowInteractions(true/false)
```

### restartApp()

Restarts the app

```typescript
await session.restartApp()
```

### getUI()

Returns the UI as an XML string

```typescript
await session.getUI()
```

### getAdbInfo()

Returns information about the adb connection (Android only)

```javascript
const adb = await session.getAdbInfo()
```

### getNetworkInspectorUrl()

Returns the URL to chrome dev tools to inspect network logs. Requires proxy to be set to `intercept`

```javascript
const url = await session.getNetworkInspectorUrl()
```

### playAction()

Play an automation Action or array of Actions.

```typescript
await session.playAction(action)
```

**Parameters**

| Name   | Type                  | Description                                                                    |
| ------ | --------------------- | ------------------------------------------------------------------------------ |
| action | `Record<string, any>` | Actions emitted from the [`session.on('action')`](api-reference.md#on-1) event |

### playAction**s**

Plays an array of actions.

```typescript
await session.playActions(actions)
```

**Parameters**

| Name    | Type                         | Description                                                                    |
| ------- | ---------------------------- | ------------------------------------------------------------------------------ |
| actions | `Array<Record<string, any>>` | Actions emitted from the [`session.on('action')`](api-reference.md#on-1) event |
