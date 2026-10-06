---
description: Save a file while an agent is driving the app, and look at the same screen.
hidden: true
---

# AI live editing

This sits in the normal development loop.

An agent has the app open. It changes JavaScript or a style, saves, and looks at the same screen. That save does not need a new build.

1. A development build is already on the device.
2. The agent edits a file and saves.
3. The screen updates.
4. The agent checks it, with `inspect` or a screenshot.
5. It edits again.

<figure><img src="../../.gitbook/assets/live-editing.svg" alt="A development server on your machine sends JavaScript to the app on Appetize through a connection. The CLI controls the device separately."><figcaption><p>The blue path is the save. The gray path is the agent looking at the device.</p></figcaption></figure>

[Metro](metro.md) is the connection we have tried for React Native. The CLI is how the agent drives the session. It does not send the code.

Use a development build of the app. Expo Go is not on the device, and a release build will not pick up the save.

## Connections

| Connection | Where it works |
| --- | --- |
| [Metro](metro.md) | Android and iOS. We have tried it on Android. |

## When you still need a new build

A native change needs one: a new native library, a change in app config, or an SDK upgrade. Upload that build, then go back to editing.

JavaScript and styles do not.

On Android the agent can install the new build into the session it already has. On iOS it uploads the build and starts a new session. See [Sessions](../sessions.md).
