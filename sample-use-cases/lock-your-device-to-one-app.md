---
description: >-
  Learn how to enable App Pinning (Kiosk Mode) on Android to lock your device to
  a single application for a more controlled previewing environment.
---

# Lock Your Device to One App

{% hint style="info" %}
App Pinning is currently only available on Android devices
{% endhint %}

App pinning, also known as Kiosk Mode, is a feature that restricts users to a single app, preventing access to other applications, settings, or the home screen. This is especially useful in scenarios where you want to restrict access to other parts of the device.&#x20;

In this guide we will cover how you can enable app pinning for the current running application using our [JavaScript SDK](broken-reference) and [adbShellCommand](../javascript-sdk/automation/device-commands.md#adbshellcommand) functionality.

## JavaScript SDK Setup

Before enabling App Pinning, you need to ensure that the Appetize JavaScript SDK is properly set up in your project. The SDK allows you to control various aspects of the device, including sending ADB shell commands.

Follow our [Getting Started](../javascript-sdk/getting-started.md) steps to set up the JavaScript SDK.

## Enabling App Pinning

Once your SDK setup is complete, you can enable App Pinning by running the following function after the session has started:

{% code title="Pin Running Application" overflow="wrap" fullWidth="false" %}
```typescript
async function pinRunningApp(session) {
    // Apply app pinning to the currently launched application
    const command = 'taskId=\$(am stack list | grep -E -o \"taskId=[0-9]+: $PACKAGE\" | grep -E -o \"[0-9]+\"); am task lock \$taskId';
    await session.adbShellCommand(command);
}
```
{% endcode %}

