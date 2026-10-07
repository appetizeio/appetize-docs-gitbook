---
description: The development loop. Save while the app is open, then look at the same screen.
hidden: true
---

# Live editing

The app is already running. Save a file. The screen updates. Look, then save again.

That is the development loop. You do it, or an agent does the same steps. It does not need a new build.

<figure><img src="../../.gitbook/assets/live-editing.svg" alt="A save goes from your editor, through a development server and a connection, to the app on Appetize. The CLI controls the device separately."><figcaption><p>The blue path is the save. The gray path is you, or an agent, driving the device.</p></figcaption></figure>

The save goes through a connection. [Metro](metro.md) is one, for React Native. The CLI starts the session and can tap the screen. It does not send the file.

Use a development build. A release build will not pick up the save.

## Connections

| Connection | For |
| --- | --- |
| [Metro](metro.md) | React Native |

## A new build

Upload a new build when the native app changes: a new native library, app config, or an SDK upgrade. Then keep editing.

On Android you can install that build into the open session. On iOS, start a new session with the new build. See [Sessions](../../ai-agents/sessions.md).
