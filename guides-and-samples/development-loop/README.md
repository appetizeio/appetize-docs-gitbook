---
description: Change the code, see it on an Appetize device, and change it again.
---

# AI Development Loop

You can run the loop, or an agent can run the same steps.

## Hot reload

A development server sends the change to the app. There is no build, and the app keeps its state. The app on the device is a development build.

<figure><img src="../../.gitbook/assets/hot-reload.svg" alt="A change goes from your machine, through a development server, to the app on Appetize. The CLI controls the device separately."><figcaption><p>The blue path is the change. The gray path is you, or an agent, driving the device.</p></figcaption></figure>

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td>React Native</td><td>Hot reload with Metro and Fast Refresh.</td><td><a href="react-native.md">react-native.md</a></td></tr></tbody></table>
