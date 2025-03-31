---
description: >-
  Learn how to enable App Pinning (Kiosk Mode) on Android to lock your device to
  a single application for a more controlled previewing environment.
---

# Lock Your Device to One App

{% hint style="info" %}
App Pinning is currently only available on Android devices
{% endhint %}

App pinning, also known as Kiosk Mode, is a feature that restricts users to a single app, preventing access to other applications, settings, or the home screen. This is especially useful in scenarios where you want to restrict access to other parts of the device.

In this guide we will cover how you can enable app pinning for the current running application using our [JavaScript SDK](../javascript-sdk/) and [adbShellCommand](../javascript-sdk/automation/device-commands.md#adbshellcommand) functionality.

## JavaScript SDK Setup

Before enabling App Pinning, you need to ensure that the Appetize JavaScript SDK is properly set up in your project. The SDK allows you to control various aspects of the device, including sending ADB shell commands.

Follow our [Getting Started](../javascript-sdk/) steps to set up the JavaScript SDK.

## Enabling App Pinning

Once the SDK is set up and a session has started, you can enable **App Pinning** to lock a specific app in the foreground. Use the function below, providing the package name of the app you want to pin.

{% code title="Pin Running Application" overflow="wrap" fullWidth="false" %}
```typescript
async function pinRunningApp(session, packageName) {
    // Apply app pinning to the currently launched application
     const command = "'taskId=$(am stack list | grep -E -m 1 -o \"taskId=[0-9]+: " + 
        packageName + 
        "\" | grep -E -o \"[0-9]+\"); am task lock $taskId'";
    await session.adbShellCommand(command);
}
```
{% endcode %}

{% hint style="info" %}
* `packageName` should be the full Android package name of the app you want to pin (e.g.`"com.example.myapp"`).
* The app **must already be running** before calling this function, as the command looks for its active task in the stack.
{% endhint %}

## Disable System Toasts (Optional)

You can choose to disable toast notifications during the session, such as the confirmation message indicating that your app has been pinned. This is optional and can help reduce distractions or clutter.

```typescript
async function disableToastMessages(session) {
    await session.adbShellCommand('appops set com.android.systemui TOAST_WINDOW deny');
}
```
