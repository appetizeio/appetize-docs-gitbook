---
description: Save a file on your computer and see it on the Appetize device.
hidden: true
---

# Live editing

You save a JavaScript or style change. The app on the device updates. You do not upload a new build.

<figure><img src="../../.gitbook/assets/live-editing.svg" alt="A development server on your machine sends JavaScript to the app on Appetize through a connection. The CLI controls the device separately."><figcaption><p>Your code takes the blue path. The CLI takes the gray path.</p></figcaption></figure>

The blue path is the code. It goes out through a connection. Today that connection is [Metro](metro.md).

The gray path is the CLI. It starts the device and can tap the screen. It does not send your code.

Use a development build of your own app. Expo Go is not on the device, and a release build cannot load new code from your computer.

## Connections

| Connection | Where it works |
| --- | --- |
| [Metro](metro.md) | Android and iOS. We have tried it on Android. |

Add a row here when another connection works. Until then, leave it out.

## When you do need a new build

Upload a new build for a native change: a new native library, a change in app config, or an SDK upgrade.

JavaScript and styles do not need one.

On Android you can install that new build into the session you already have. On iOS, upload it and start a new session. See [Sessions](../../ai-agents/sessions.md).
