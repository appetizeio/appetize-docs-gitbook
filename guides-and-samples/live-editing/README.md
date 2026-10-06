---
description: >-
  Keep a development build running on Appetize and apply JavaScript changes
  from your machine. Metro is the first connection. Add another when it works.
---

# Live editing

Appetize runs the native app. A development server on your machine serves its JavaScript. Saving a JavaScript or styling change updates the running app. Upload a new build only when the native app itself changes.

The CLI starts the device and drives it. It does not serve JavaScript, and it does not open a tunnel to your development server. Each page in this section is one way to connect the device to that server.

<figure><img src="../../.gitbook/assets/live-editing.svg" alt="Editor saves reach a development server on your machine. JavaScript crosses a connection option, Metro's tunnel today, into the development build on Appetize. The Appetize CLI reaches that same build with the session, taps, and screenshots, and does not carry the JavaScript."><figcaption><p>JavaScript crosses a connection option. The CLI only controls the device.</p></figcaption></figure>

Use your own development build. Expo Go is not required, and Appetize devices do not include it. A release build cannot load a development server.

## Options

| Option | What it connects | Platforms |
| --- | --- | --- |
| [Metro](metro.md) | An Expo development build to a local Metro server, through Expo's tunnel | Android and iOS. Android has been run end to end. iOS uses the same URL once a simulator build is uploaded. |

Add a page under this section, and a row in the table, when another connection has been shown to work. Say which platforms it covers. Leave the row out until then.

When a step is easier to judge by looking than by reading the commands, put a screenshot or a short recording on that option's page.

## What still needs a new build

Upload a new native build after any of these changes:

* a native dependency is added or upgraded
* `app.json`, a config plugin, or an entitlement changes
* the Expo SDK or React Native version changes

JavaScript, TypeScript, and styling changes do not need a new upload.

On Android, `session start` prints `adbSerial`, so you can replace the installed app without ending the session. iOS has no equivalent install command: upload the new simulator build and start a session against its build id. See [Sessions](../../ai-agents/sessions.md).
