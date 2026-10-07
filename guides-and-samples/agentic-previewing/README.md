---
description: An agent saves a change while the app is open, then checks the same screen.
hidden: true
---

# Agentic Previewing

The app is already running on Appetize. The agent saves a file. The screen updates. It looks, then saves again.

That is the development loop, and you can run it by hand too. It does not need a new build.

<figure><img src="../../.gitbook/assets/agentic-previewing.svg" alt="A save goes from your editor, through a development server and a connection, to the app on Appetize. The CLI controls the device separately."><figcaption><p>The blue path is the save. The gray path is you, or an agent, driving the device.</p></figcaption></figure>

The save goes through a connection. [Metro](metro.md) is one, for React Native. The CLI starts the session and can tap the screen. It does not send the file.

Use a development build. A release build will not pick up the save.

## Connections

| Connection | For |
| --- | --- |
| [Metro](metro.md) | React Native |

## A new build

Upload a new build when the native app changes: a new native library, app config, or an SDK upgrade. Then keep editing.

On Android you can install that build into the open session. On iOS, start a new session with the new build. See [Sessions](../../ai-agents/sessions.md).
