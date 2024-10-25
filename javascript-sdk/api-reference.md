# API reference

## getClient(selector)

Get an instance of the Appetize client.

```javascript
const client = await window.appetize.getClient('#my_iframe')
```

**Parameters**

| Name     | Type     | Description                                             |
| -------- | -------- | ------------------------------------------------------- |
| selector | `string` | A query selector string pointing to the embedded iframe |

## getClient(selector, config)

Get an instance of the Appetize client as well as set the initial config when loading the client.

_Useful when the embed link might not be known up front and the configuration has to be applied at runtime._

```javascript
const client = await window.appetize.getClient('#my_iframe', {
    buildId: '{buildId|publicKey}',
    device: 'iphone11pro',
    osVersion: '15.0'
    ...
})
```

**Parameters**

| Name     | Type                  | Description                                                                                                  |
| -------- | --------------------- | ------------------------------------------------------------------------------------------------------------ |
| selector | `string`              | A query selector string pointing to the embedded iframe                                                      |
| config   | `Record<string, any>` | A JSON object describing the [Configuration options](configuration.md#configuration-options) for the device. |

## Client

### on() <a href="#on-client" id="on-client"></a>

Listens for an event of the given name

```typescript
client.on(event, data => {
   console.log(data)
})
```

| Event                | Data Type                                             | Description                                                                                                  |
| -------------------- | ----------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| **queue**            | <p><code>{</code><br><code>type: 'session'</code></p> | <p>'concurrent',</p><p><code>position: number,</code></p><p><code>name?: string</code><br><code>}</code></p> |
| **error**            | `string`                                              | An error has occurred                                                                                        |
| **deviceInfo**       | `Record<string, any>`                                 | Information about the current device, such as type, osVersion, and screen dimensions.                        |
| **sessionRequested** | `void`                                                | A new session has been requested either by the client or user clicking "Tap to Play"                         |
| **sessionEnded**     | `void`                                                | An active session has ended.                                                                                 |
| **session**          | `Session`                                             | A new session has started either by the client or user clicking "Tap to Play"                                |
| **app**              | `Record<string, any>`                                 | The currently loaded Appetize app                                                                            |

### startSession()

Starts a session with the requested app, device, operating system, and other launch options.

```typescript
const session = await client.startSession()
```

**Parameters**

| Name      | Type                  | Description                                                                                                  |
| --------- | --------------------- | ------------------------------------------------------------------------------------------------------------ |
| `config?` | `Record<string, any>` | A JSON object describing the [Configuration options](configuration.md#configuration-options) for the device. |

### setConfig()

Update the configured app, device, operating system, or other launch options.

_Note: This will end any active sessions._

```typescript
await client.setConfig(config)
```

**Parameters**

| Name     | Type                  | Description                                                                                                  |
| -------- | --------------------- | ------------------------------------------------------------------------------------------------------------ |
| `config` | `Record<string, any>` | A JSON object describing the [Configuration options](configuration.md#configuration-options) for the device. |

### getConfig()

Returns the current config

```javascript
const config = client.getConfig()
```

### endSession()

Ends the active session or cancels any pending session requests.

```typescript
await client.endSession()
```

### device

The currently loaded device

```typescript
{
    type: string;
    name: string;
    osVersion: string;
    orientation: 'portrait' | 'landscape';
    screen: {
        width: number;
        height: number;
        devicePixelRatio?: number;
    };
    embed: {
        width: number;
        height: number;
        screen: {
            width: number;
            height: number;
            offset: {
                x: number;
                y: number;
            };
        };
    };    
}
```

### app

The currently loaded app

```typescript
{
  buildId: string;
  name?: string;
  appDisplayName?: string;
  appVersionName?: string;
  appVersionCode?: string;
  bundle?: string;
  platform?: string;
  versionCode?: string;
  architectures?: string;
  iconUrl?: string;
  created?: string;
  apps?: AppetizeApp[];
}
```

## **Session**

### on() <a href="#on-session" id="on-session"></a>

Listens for an event of the given name

```typescript
session.on(event, data => {
   console.log(data)
})
```

| Event                  | Data Type                                                                                                                                                                | Description                                                                                                                                                                                                                                                                                        |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **action**             | `Record<string, any>`                                                                                                                                                    | <p>A user action has been recorded. This can be played back later with <a href="api-reference.md#playaction-action-options">playAction</a>.<br><br>Requires <a href="configuration.md#record">record</a> to be set to <code>true</code></p>                                                        |
| **audio**              | <p><code>{</code><br><code>buffer: Uint8Array, codec: 'aac'</code><br><code>}</code></p>                                                                                 | <p>Audio frames of the current session.<br><br>Requires <a href="configuration.md#audio">audio</a> to be set to <code>true</code></p>                                                                                                                                                              |
| **error**              | `string`                                                                                                                                                                 | An error has occurred on the session                                                                                                                                                                                                                                                               |
| **inactivityWarning**  | `{ secondsRemaining: number }`                                                                                                                                           | <p>Session is about to timeout due to inactivity.</p><p>Any user interaction or a <a href="api-reference.md#heartbeat">heartbeat</a> will reset the timeout.</p>                                                                                                                                   |
| **interaction**        | `Record<string, any>`                                                                                                                                                    | User has interacted with the device.                                                                                                                                                                                                                                                               |
| **log**                | `{ message: string }`                                                                                                                                                    | <p>Debug log from the device<br><br>Requires <a href="configuration.md#debug">debug</a> to be set to <code>true</code></p>                                                                                                                                                                         |
| **network**            | `Record<string, any>`                                                                                                                                                    | <p>Intercepted network request or responses.<br></p><p>Requires <a href="configuration.md#proxy">proxy</a> to be set to <code>intercept</code></p>                                                                                                                                                 |
| **orientationChanged** | `'portrait' \| 'landscape'`                                                                                                                                              | The device has changed orientation                                                                                                                                                                                                                                                                 |
| **video**              | <p><code>{</code><br><code>buffer: Uint8Array,</code><br><code>width: number,</code><br><code>height: number,</code><br><code>codec: string</code><br><code>}</code></p> | <p>Video frames of the current session.<br><br>These frames can be muxed (e.g. using <a href="https://github.com/samirkumardas/jmuxer">jmuxer</a>) to turn it into a video format.<br><br>When <a href="configuration.md#codec">codec</a> is <code>jpeg</code> the buffers are of jpeg images.</p> |
| **end**                | `void`                                                                                                                                                                   | The session has ended                                                                                                                                                                                                                                                                              |

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

### screenshot(format)

Takes a screenshot of the device and returns the data

```typescript
const { data, mimeType } = await session.screenshot(format)
```

**Parameters**

| Name    | Type                   | Description                                                       |
| ------- | ---------------------- | ----------------------------------------------------------------- |
| format? | `"buffer" \| "base64"` | The format of the screenshot data to return. Defaults to `buffer` |

### heartbeat()

Sends a heartbeat to the server, resetting the inactivity timer

```typescript
await session.heartbeat()
```

### tap(target, options)

Taps on the screen at the given position, coordinate or element

```typescript
await session.tap({ position: { x: '50%', y: '50%' } })
await session.tap({ coordinates: { x: 100, y: 100 } })
await session.tap({ element: { attributes: { text: 'OK' } } })
```

**Parameters**

| Name                | Type                                                                                           | Description                                                                                 |
| ------------------- | ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| target.coordinates? | <p><code>{</code><br><code>x: number</code><br><code>y: number</code></p><p><code>}</code></p> | The coordinates in dip units                                                                |
| target.position?    | <p><code>{</code><br><code>x: string</code><br><code>y: string</code><br><code>}</code></p>    | The position on screen in %                                                                 |
| target.element?     | `ElementSelector`                                                                              | An [element selector](automation/touch-interactions.md#targeting-elements)                  |
| target.duration?    | `number`                                                                                       | Duration of the tap                                                                         |
| options.timeout?    | `number`                                                                                       | If an element is provided, the amount of time to wait for it to appear in ms (defaults 10s) |
| options.matchIndex? | `number`                                                                                       | If multiple elements match the element selector, select the nth one                         |

### swipe(target, options)

Swipes on the screen at the given position, coordinate or element

```typescript
await session.swipe({ position: { x: '50%', y: '50%' }, gesture: 'up' })
await session.swipe({ coordinates: { x: 100, y: 100 }, gesture: 'up' })
await session.swipe({ element: { attributes: { text: 'OK' } }, gesture: 'up' })
```

|                     |                                                                                                |                                                                                                |
| ------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| target.coordinates? | <p><code>{</code><br><code>x: number</code><br><code>y: number</code></p><p><code>}</code></p> | The coordinates in dip units to start the swipe                                                |
| target.position?    | <p><code>{</code><br><code>x: string</code><br><code>y: string</code><br><code>}</code></p>    | The position on screen in %                                                                    |
| target.element?     | `ElementSelector`                                                                              | An [element selector](automation/touch-interactions.md#targeting-elements)                     |
| target.duration?    | `number`                                                                                       | Duration of the swipe                                                                          |
| target.gesture      | `string \| function`                                                                           | The gesture of the swipe. See [swipe](automation/touch-interactions.md#swipe) for more details |
| options.timeout?    | `number`                                                                                       | If an element is provided, the amount of time to wait for it to appear in ms (defaults 10s)    |
| options.matchIndex? | `number`                                                                                       | If multiple elements match the element selector, select the nth one                            |

### type(text)

Types the given text on the device

```typescript
await session.type("hello")
```

**Parameters**

| Name | Type     | Description  |
| ---- | -------- | ------------ |
| text | `string` | Text to type |

{% hint style="warning" %}
Typing is limited to 1000 characters at a time to ensure optimal performance and prevent potential disruptions. For larger payloads, you can use multiple 'type' operations.
{% endhint %}

### keypress(character, options)

Sends a single key press to the device

```typescript
await session.keypress("a")
```

**Parameters**

| Name           | Type      | Description                                                                                                                                                                                                                                             |
| -------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| key            | `string`  | <p>Key to send to the device ('a', 'b', etc.)<br><br>Also takes special values for hardware keys:<br><br><code>HOME</code><br><code>VOLUME_UP</code> (android only)<br><code>VOLUME_DOWN</code> (android only)<br><code>ANDROID_KEYCODE_MENU</code></p> |
| options.shift? | `boolean` |                                                                                                                                                                                                                                                         |

### setLanguage(language)

Changes the current language and restarts the app

```typescript
await session.setLanguage("fr")
```

{% hint style="warning" %}
If your app does not automatically handle language/locale changes, you would need to explicitly call [restartApp](api-reference.md#restartapp) for this to take effect.\
\
Some apps might also cache data in the previously used language. In these cases use [reinstallApp](api-reference.md#reinstallapp) to clear any previous cached data.
{% endhint %}

**Parameters**

| Name     | Type     | Description   |
| -------- | -------- | ------------- |
| language | `string` | Language code |

### setLocation(lat, long)

Sets the simulated location of the device.

```typescript
await setLocation(-33.924434, 18.418391)
```

#### Parameters

| Name      | Type     | Description                                                                                                                                                                                                          |
| --------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| latitude  | `number` | Decimal number between -90 and 90, representing the degrees of north or south of the Equator. Negative numbers indicate south of the Equator, and positive numbers indicate north of the Equator.                    |
| longitude | `number` | Decimal number between -180 and 180, representing the degrees of east or west of the Prime Meridian. Negative numbers indicate west of the Prime Meridian, and positive numbers indicate east of the Prime Meridian. |

### openUrl(url)

Opens a deep-link or web URL

```typescript
await session.openUrl("https://appetize.io")
```

**Parameters**

| Name  | Type     | Description |
| ----- | -------- | ----------- |
| `url` | `string` | The URL     |

### shake()

Shakes device

```typescript
await session.shake()
```

### toggleSoftKeyboard()

Toggles the soft keyboard (iOS only)

```typescript
await session.toggleSoftKeyboard()
```

### biometryEnrollment(isEnrolled)

Sets the biometry enrollment status (_iOS Only_)

```typescript
await session.biometryEnrollment(true/false)
```

### biometry(match)

Simulate a matching fingerprint (Android 8+ only) or Face ID (iOS)

<pre class="language-typescript"><code class="lang-typescript">await session.biometry({
<strong>    match: true/false
</strong>})
</code></pre>

### allowInteractions(enabled)

Enables or disables all interactions on the device. Default is true.

```typescript
await session.allowInteractions(true/false)
```

### launchApp(appId)

Launches the specified application using the provided `appId`.

{% hint style="info" %}
If the app is already running, it will be brought to the foreground instead of being relaunched. If the app was originally launched with params or a launchUrl, these will also be passed with this method.
{% endhint %}

```typescript
await session.launchApp(appId)
```

**Parameters**

| Name    | Type     | Description                                                                                                                                                                                                                                                                                                                |
| ------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `appId` | `string` | <p><strong>Android:</strong><br>The app's package name / appId (e.g., <code>com.example.app</code>) or <code>packageName/activityName</code>. If no activity name is specified, it defaults to the main launch activity.<br><strong>iOS:</strong><br>The app's bundle identifier (e.g., <code>com.example.app</code>).</p> |

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

### getUI()

Returns the UI as an XML string

```typescript
await session.getUI()
```

{% hint style="warning" %}
**Experimental**\
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

### addMedia(file)

{% hint style="info" %}
The maximum file size for uploading media is **50 MB**.
{% endhint %}

Upload media to the device.

```typescript
await session.addMedia(file)
```

### playAction(action, options)

Play an automation Action or array of Actions.

```typescript
await session.playAction(action)
```

**Parameters**

| Name             | Type                  | Description                                                                    |
| ---------------- | --------------------- | ------------------------------------------------------------------------------ |
| action           | `Record<string, any>` | Actions emitted from the [`session.on('action')`](api-reference.md#on-1) event |
| options.timeout? | `number`              | Amount of time in ms to wait for the action to succeed (default 10s)           |

### playAction**s(actions, options)**

Plays an array of actions.

```typescript
await session.playActions(actions)
```

**Parameters**

| Name             | Type                         | Description                                                                    |
| ---------------- | ---------------------------- | ------------------------------------------------------------------------------ |
| actions          | `Array<Record<string, any>>` | Actions emitted from the [`session.on('action')`](api-reference.md#on-1) event |
| options.timeout? | `number`                     | Amount of time in ms to wait for an action to succeed (default 10s)            |

### waitForAnimations(options)

Waits until the there are no ongoing animations on the screen by waiting for the image to stabilize for at least 1 second.

```typescript
await session.waitForAnimations(options)
```

**Parameters**

| Name                    | Type     | Description                                                                                                                                         |
| ----------------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| options.imageThreshold? | `number` | <p>The threshold for the amount of pixels (in %) that can change between frames before the image is considered to be stable.<br>(default 0.001)</p> |
| options.timeout?        | `number` | <p>The maximum amount of time (in ms) to wait for the image to stabilize.<br>(default 10s)</p>                                                      |

### adbConnection

Info for connecting to the Android devices via adb. Requires [enableAdb](configuration.md#enableadb) to be true

```typescript
{
    command: string;
    forwards: Array<{ destination: string; port: number }>;
    hash: string;
    hostname: string;
    port: number;
    user: string;
}
```

### networkInspectorUrl

The URL to chrome dev tools to inspect network logs. Requires [proxy](configuration.md#proxy) to be set to `intercept`

### device

The current device

```typescript
{
    type: string;
    name: string;
    osVersion: string;
    orientation: 'portrait' | 'landscape';
    screen: {
        width: number;
        height: number;
        devicePixelRatio?: number;
    };
    embed: {
        width: number;
        height: number;
        screen: {
            width: number;
            height: number;
            offset: {
                x: number;
                y: number;
            };
        };
    };    
}
```

### app

The Appetize app for the session

```typescript
{
  publicKey|buildId: string;
  name?: string;
  appDisplayName?: string;
  appVersionName?: string;
  appVersionCode?: string;
  bundle?: string;
  platform?: string;
  versionCode?: string;
  architectures?: string;
  iconUrl?: string;
  created?: string;
  apps?: AppetizeApp[];
}
```

### path

The URL to the Appetizer server

### token

The token of the Appetize session
