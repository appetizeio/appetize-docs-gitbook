---
description: >-
  The client provides methods to configure the embedded device, manage sessions
  and listen to device related events.
---

# Client

## Methods <a href="#on-client" id="on-client"></a>

### on(event, listener) <a href="#on-client" id="on-client"></a>

Listens for an event of the given name

```typescript
client.on(event, data => {
   console.log(data)
})
```

<table data-full-width="false"><thead><tr><th>Event</th><th>Data Type</th><th>Description</th></tr></thead><tbody><tr><td><h4><strong>app</strong></h4></td><td><a href="types/appetizeapp.md">AppetizeApp</a></td><td>The currently loaded <a href="client.md#app-1">Appetize app</a>.</td></tr><tr><td><h4><strong>deviceInfo</strong></h4></td><td><a href="types/deviceinfo.md">DeviceInfo</a></td><td>Information about the current <a href="client.md#device">device</a>, such as type, osVersion, and screen dimensions.</td></tr><tr><td><h4><strong>error</strong></h4></td><td><code>{ message: string }</code></td><td>An error has occurred</td></tr><tr><td><h4><strong>queue</strong></h4></td><td><code>{</code> <br>  <code>type: "session | concurrent",</code> <br>  <code>position: number,</code><br>  <code>name: string</code> <br><code>}</code></td><td><p>Your position in queue for the device.</p><ul><li><strong>concurrent</strong>: You've reached the max concurrent sessions for your account and are waiting for the next available slot. The concurrent queue <strong>name</strong> will be shown.</li><li><strong>session</strong>: You're in a queue, waiting for the next available device.</li></ul></td></tr><tr><td><h4>queueEnd</h4></td><td><code>void</code></td><td>The active queue has ended.</td></tr><tr><td><h4><strong>session</strong></h4></td><td><code>Session</code></td><td>A new <a href="session.md">session</a> has started either by the client or user clicking "Tap to Play"</td></tr><tr><td><h4><strong>sessionEnded</strong></h4></td><td><code>void</code></td><td>An active session has ended.</td></tr><tr><td><h4><strong>sessionRequested</strong></h4></td><td><code>void</code></td><td>A new session has been requested either by the client or user clicking "Tap to Play"</td></tr></tbody></table>

### startSession()

Starts a session with the requested app, device, operating system, and other launch options.

```typescript
const session = await client.startSession()
```

**Parameters**

| Name      | Type                                    | Description                                                                                                     |
| --------- | --------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| `config?` | [SessionConfig](types/sessionconfig.md) | A JSON object describing the [Configuration options](../configuration.md#configuration-options) for the device. |

### setConfig()

Update the configured app, device, operating system, or other launch options.

_Note: This will end any active sessions._

```typescript
await client.setConfig(config)
```

**Parameters**

| Name     | Type                                    | Description                                                                                                     |
| -------- | --------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| `config` | [SessionConfig](types/sessionconfig.md) | A JSON object describing the [Configuration options](../configuration.md#configuration-options) for the device. |

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

## Properties

### device

The currently loaded device. See [DeviceInfo](types/deviceinfo.md).

### app

The currently loaded app. See [AppetizeApp](types/appetizeapp.md).

