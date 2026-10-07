---
description: Change the code, see it on an Appetize device, and change it again.
hidden: true
---

# Development loop

You can run the loop, or an agent can run the same steps.

<figure><img src="../../.gitbook/assets/development-loop.svg" alt="A change reaches the app on Appetize by hot reload, with no build, or by a new build installed on the device. The CLI controls the device separately."><figcaption><p>A change reaches the app in one of two ways. The CLI drives the device. It does not carry the change.</p></figcaption></figure>

## Hot reload

Use this for code a development server sends to the app, such as React Native JavaScript. The change shows up without a build, and the app keeps its state. The app on the device must be a development build.

## A new build

Use this for native code, a new native library, or app config. Build the app again, then put it on the device.

On Android, install it into the open session with `adb install`. See [adb](../../ai-agents/sessions.md#adb). On iOS, start a new session with the new build.

## Guides

Pick the guide for your app.

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td>React Native</td><td>Hot reload with Metro and Fast Refresh. No build for JavaScript changes.</td><td><a href="react-native.md">react-native.md</a></td></tr></tbody></table>
