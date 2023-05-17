---
description: Interact with the virtual device via a Javascript post-message API
---

# Cross-document messages

{% hint style="danger" %}
Cross-document messages API is no longer receiving updates.&#x20;

Please use our [Javascript SDK](../javascript-sdk/getting-started.md) for any new development.
{% endhint %}

Cross-document messaging, when enabled via the `&xdocMsg=true` query parameter, allows you to issue commands to the embedded iFrame via Javascript via [`postMessage(message, targetOrigin)`](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage).

Messages without any parameters can be passed directly as strings, e.g.

```typescript
postMessage('requestSession', '*')
```

Messages with parameters should be passed as objects with the message name in the `type` field. E.g.

```typescript
postMessage({ type: 'mouseclick', x: 100, y:100 }, '*')
```

## Sendable Messages

### requestSession

Equivalent to clicking play

```typescript
postMessage('requestSession', '*')
```

### emitHomeButton

Taps the home button for iOS apps when available

```typescript
postMessage('emitHomeButton', '*')
```

### rotateLeft

Rotates counter-clockwise

```typescript
postMessage('rotateLeft', '*')
```

### rotateRight

Rotates clockwise

```typescript
postMessage('rotateRight', '*')
```

### setScale

Sets device scale to a value between 10 and 100

```typescript
postMessage({ type: 'setScale', value: 50 })
```

### saveScreenshot

Prompts user to download screenshot

```typescript
postMessage('saveScreenshot', '*')
```

### getScreenshot

Sends screenshot data directly to parent window. See the `screenshot` event the iFrame posts to the parent.

```typescript
postMessage('getScreenshot', '*')
```

### heartbeat

Sends heartbeat to prevent inactivity timeout

```typescript
postMessage('heartbeat', '*')
```

### mouseclick

Sends click event at the provided coordinates

```typescript
postMessage({ type: 'mouseclick', x: 100, y:100 }, '*')
```

### pasteText

Pastes the provided text

```typescript
postMessage({ type: 'pasteText', value: 'Hello World' }, '*')
```

### keypress

Sends keypress. `key` should be a string that identifies the key pressed, e.g. `'a'`. Acceptable values on Android also include `'volumeUp'` and `'volumeDown'`.

```typescript
postMessage({ type: 'keypress', key: 'a', shiftKey: true }, '*') // would send 'A"
```

### language

Sets language, restarts app

```typescript
postMessage({ type: 'language', value: 'fr' }, '*')
```

### location

Sets location. `value` should be 2-length array that contains \[latitude, longitude]

```typescript
postMessage({ type: 'location', value: [50.0, -100.0] }, '*')
```

### url

Opens deep-link or regular URL in Safari

```typescript
postMessage({ type: 'url', value: 'https://appetize.io' }, '*')
```

### shakeDevice

Send shake gesture to iOS apps

```typescript
postMessage('shakeDevice', '*')
```

### androidKeycodeMenu

Sends Android KEYCODE\_MENU command

```typescript
postMessage('androidKeycodeMenu', '*')
```

### adbShellCommand

Executes an adb shell command on an Android device.

If a session is already running the command will be executed immediately. If the session has not been started, the command will execute upon start.

```typescript
postMessage({ 
    type: 'adbShellCommand', 
    value: 'am start -a android.intent.action.VIEW -d https://appetize.io/'
}, '*')
```

### biometryMatch

(Android 8+ only) simulate a matching fingerprint

```typescript
postMessage('biometryMatch', '*')
```

### biometryNonMatch

(Android 8+ only) simulate a non-matching fingerprint

```typescript
postMessage('biometryNonMatch', '*')
```

### disableInteractions

Disables all user interactions

```typescript
postMessage('disableInteractions', '*')
```

### enableInteractions

Re-enables all user interactions

```typescript
postMessage('enableInteractions', '*')
```

### restartApp

Kills and restarts app in same session

```typescript
postMessage('restartApp', '*')
```

### endSession

Ends the session

```typescript
postMessage('endSession', '*')
```

## Receivable Messages

The iFrame also posts messages to the parent window via `message` event. You can listen for them with an event handler on the window:

```typescript
window.addEventListener('message', (event) => {    
    const type = typeof event.data === 'string' ? event.data : event.data.type
    
    console.log(type)
})
```

### userInteractionReceived

Session has received an interaction from the user

```typescript
{
    data: {
        type: "userInteractionReceived",
        value: {
            altKey: boolean,
            shiftKey: boolean,
            timeStamp: number,
            type: string,
            xPos: number,
            yPost: number
        }
    }
}
```

### heartbeatReceived

Heartbeat event received

```typescript
{
    data: "heartbeatReceived"
}
```

### orientationChanged

Device orientation has changed

```typescript
{
    data: { 
        type: "orientationChanged",
        value: "landscape" | "portrait"
    }
}
```

### sessionRequested

Session has been requested

```typescript
{
    data: "sessionRequested"
}
```

### userError

An error occurred while starting session

```typescript
{
    data: { 
        type: "userError",
        value: string // error message
    }
}
```

### sessionQueued

You have entered a system-level queue (awaiting device availability)

```typescript
{
    data: "sessionQueued"
}
```

### sessionQueuedPosition

Position of session queue

```typescript
{
    data: { 
        type: "sessionQueuedPosition",
        position: number
    }
}
```

### accountQueued

You have entered an account-level queue (concurrent users)

```typescript
{
    data: "accountQueued"
}
```

### accountQueuedPosition

Account queue position

```typescript
{
    data: { 
        type: "accountQueuedPosition",
        position: number
    }
}
```

### appLaunch

App launch command sent

```typescript
{
    data: "appLaunch"
}
```

### firstFrameReceived

First frame received

```typescript
{
    data: "firstFrameReceived"
}
```

### timeoutWarning

Session is about to timeout in 10 seconds

```typescript
{
    data: "timeoutWarning"
}
```

### sessionEnded

Session has ended

```typescript
{
    data: "sessionEnded"
}
```

### screenshot

Screenshot data received

```typescript
{
    data: {
        type: "screenshot",
        data: string // base64 encoded image data
    }
}
```

### sessionConnecting

Passes the identifying token for the session

```typescript
{
    data: { 
        type: "sessionConnecting",
        token: string,
        path: string
    }
}
```

### chromeDevToolsUrl

URL to view dev tools for the device (only if network intercept enabled)

```typescript
{
    data: { 
        type: "chromeDevToolsUrl",
        value: string
    }
}
```

### interceptResponse

Intercepted network response.

This is only emitted if network intercept enabled (`proxy=intercept` query param)

```typescript
{
    data: { 
        type: "interceptResponse",
        value: {
            cache: object
            request: {
                bodySize: number
                cookies: Array<{ name: string, value: string }>
                headers: Array<{ name: string, value: string }>
                headersSize: number
                httpVersion: string
                method: string
                queryString: Array<{ name: string, value: string }>
                url: string
            }
            requestId: string
            serverIPAddress: string
        }
    }
}
```

### interceptRequest

Intercepted network request.

This is only emitted if network intercept enabled (`proxy=intercept` query param)

```typescript
{
    data: { 
        type: "interceptRequest",
        value: {
            cache: object
            request: {
                bodySize: number
                cookies: Array<{ name: string, value: string }>
                headers: Array<{ name: string, value: string }>
                headersSize: number
                httpVersion: string
                method: string
                queryString: Array<{ name: string, value: string }>
                url: string
            }
            requestId: string
            serverIPAddress: string
        }
    }
}
```

### debug

Logged messages from the device.

This is only emitted if debug log is enabled (`debug=true` query param)

```typescript
{
    data: {
        type: "debug",
        value: string
    }
}
```

### deviceDimensions

The dimensions of the current device. If the `screenOnly` query param is true, the dimensions will be for the screen.

```typescript
{
    data: {
        type: "deviceDimensions",
        value: {
            width: number,
            height: number
        }
    }
}
```

### app

Information for the application

```typescript
{
    data: {
        type: "app",
        value: {
            name: "Example",
            appDisplayName: "Example",
            bundle: "com.example.app",
            publicKey: "p7nww3n6ubq73r1nh9jtauqy8w",
            platform: "ios"
        }
    }
}
```

[Check out our JSFiddle.net example to see these messages in action!](https://jsfiddle.net/appetize/f97hs3ru/)
