---
description: >-
  The ADB tunnel feature allows you to create an SSH tunnel to a running
  Appetize Android session, enabling you to interact with the device via Android
  Studio or standard ADB protocol.
---

# ADB tunnel

## Enable ADB Tunnel

To enable the ADB tunnel feature, you can either choose to enable it through a query parameter or by utilizing the JavaScript SDK.

{% hint style="warning" %}
Enabling the SSH ADB tunnel has a limitation that causes our ADB connection to terminate. Consequently, the following Appetize features will be affected and unavailable:

1. [AppRecorder](../../ui-automation.md)
2. [Screenshots](../../../javascript-sdk/api-reference.md#screenshot-format)
3. [Debug Logs](../../debug-logs.md)

If you would like to use any of these features, we recommend using [adbShellCommand](../../../javascript-sdk/automation/device-commands.md#adbshellcommand) from our JavaScript SDK instead.
{% endhint %}

### With Query Parameter

Add the `debug=true` query parameter to your app or embed URL

```uri
&enableAdb=true
```

See [Query Params Reference](../../query-params-reference.md#enableadb) for more information.

### With JavaScript SDK

Set `enableAdb: true` in the configuration e.g.

```typescript
await client.setConfig({
    enableAdb: true,
    ...
})
```

See [Configuration](../../../javascript-sdk/configuration.md#enableadb) for more information.

## Usage

### With App Page

{% hint style="info" %}
One common practice is to use the ADB tunnel to connect to an Android "standalone" device, without any specific app installed. For more information see [Standalone Device](../../../platform/standalone-device.md).
{% endhint %}

The app page provides a simple way to retrieve the `adb` information required to connect to the device.&#x20;

You can access this via your app's app link

{% code overflow="wrap" %}
```url
https://appetize.io/app/{appId|buildId|publicKey}?&enableAdb=true
```
{% endcode %}

or by going to your [Apps](https://appetize.io/apps) page, selecting `Play` on the app you want to inspect, and then toggling `Adb Tunnel` to `On`

<figure><img src="../../../.gitbook/assets/image (24).png" alt=""><figcaption><p>Select <code>Play</code> on the app you want to inspect</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/Screenshot 2023-10-24 115916.png" alt="Example ADB Tunnel Action Switched to On"><figcaption><p>Toggle ADB tunnel to "On"</p></figcaption></figure>

Select `Tap To Play` (or your equivalent text to start the session). A command will then be generated that you need to copy and paste in your shell environment e.g.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-10-24 115910.png" alt="Example command to paste in shell environment"><figcaption></figcaption></figure>

Then, the Appetize virtual Android device will appear with `adb devices`, as if it were a device plugged into your computer via USB.

### With JavaScript SDK

You can retrieve all the information needed to start an ADB session via the `adbConnection` property

```typescript
const adbInfo = session.adbConnection
const command = adbInfo.command
```

See our JavaScript [API Reference](../../../javascript-sdk/api-reference.md#adbconnection) for more information.
