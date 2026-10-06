---
description: The edit, look, and edit again loop while an agent is driving the app.
hidden: true
---

# AI live editing

This is part of development, not a separate mode.

An agent already has the app open. It changes the code, looks at the screen, and changes the code again. For JavaScript and styles, that loop does not upload a new build.

1. A development build is on the device.
2. The agent edits a file and saves.
3. The screen updates.
4. The agent checks it, with `inspect` or a screenshot.
5. It edits again.

<figure><img src="../../.gitbook/assets/live-editing.svg" alt="A development server on your machine sends JavaScript to the app on Appetize through a connection. The CLI controls the device separately."><figcaption><p>The blue path is the code the agent just saved. The gray path is the agent looking at the device.</p></figcaption></figure>

The blue path is how the save reaches the app. Today that connection is [Metro](metro.md). The gray path is the CLI the agent is already using to drive the session.

Use a development build of the app. Expo Go is not on the device, and a release build cannot pick up a new save.

## Connections

| Connection | Where it works |
| --- | --- |
| [Metro](metro.md) | Android and iOS. We have tried it on Android. |

Add a row when another connection works. Leave it out until then.

## When the loop needs a new build

A native change breaks the loop: a new native library, a change in app config, or an SDK upgrade. Upload a new build, then go back to editing.

JavaScript and styles do not need one.

On Android the agent can install that build into the session it already has. On iOS it uploads the build and starts a new session. See [Sessions](../sessions.md).
