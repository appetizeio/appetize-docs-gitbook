---
description: Interact with the virtual device via aJavascript post-message API
---

# Cross-document messages

Cross-document messaging, when enabled above, allows you to issue commands to the embedded iFrame via the javascript window [`postMessage(message, targetOrigin)`](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage) function.

Messages without any parameters can be passed directly as strings, e.g. `postMessage('requestSession', '*')`. 

Messages with parameters should be passed as objects with the message name in the `type` field. E.g. `postMessage({type: 'mouseclick', x: 100, y:100}, '*')`

* `requestSession` - equivalent to clicking play
* `emitHomeButton` - taps the home button for iOS apps
* `rotateLeft` - rotates counter-clockwise
* `rotateRight` - rotates clockwise
* `setScale(value)` - sets device scale, values between 10 and 100
* `saveScreenshot` - prompts user to download screenshot
* `getScreenshot` - sends screenshot data directly to parent window. See the `screenshot` event the iframe posts to the parent.
* `heartbeat` - sends heartbeat to prevent timeout
* `mouseclick(x, y)` - sends click event at point \(x,y\)
* `pasteText(value)` - pastes text. `value` should be a string.
* `keypress(key, shiftKey)` - sends keypress. `key` should be a string that identifies the key pressed, e.g. `'a'`. Acceptable values on Android also include `'volumeUp'` and `'volumeDown'`.
* `language(value)` - sets language, restarts app
* `location(value)` - sets location. `value` should be 2-length array that contains \[latitude, longitude\]
* `openUrl(value)` - opens deep-link or regular URL
* `shakeDevice` - send shake gesture to iOS apps
* `androidKeycodeMenu` - sends Android KEYCODE\_MENU command
* `biometryMatch` - \(Android 8+ only\) simulate a matching fingerprint
* `biometryNonMatch` - \(Android 8+ only\) simulate a non-matching fingerprint
* `disableInteractions` - disables all user interactions
* `enableInteractions` - re-enables all user interactions
* `restartApp` - kills and restarts app in same session
* `endSession` - ends the session

The iframe also posts messages to the parent window.

* `userInteractionReceived` - interaction received
* `heartbeatReceived` - heartbeat received
* `orientationChanged` - portrait or landscape
* `sessionRequested` - session requested
* `userError` - error starting session
* `sessionQueued` - system-level queue \(awaiting device availability\)
* `sessionQueuedPosition` - queue position
* `accountQueued` - account-level queue \(concurrent users\)
* `accountQueuedPosition` - queue position
* `appLaunch` - app launch command sent
* `firstFrameReceived` - first frame received
* `timeoutWarning` - timeout in 10 seconds
* `sessionEnded` - session ended
* `screenshot` - screenshot data received
* `chromeDevToolsUrl` - only if network intercept enabled
* `sessionConnecting` - passes the identifying token for the session

[Check out our JSFiddle.net example to see these messages in action!](https://jsfiddle.net/appetize/f97hs3ru/)

