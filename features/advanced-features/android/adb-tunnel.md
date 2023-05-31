---
description: >-
  The ADB tunnel feature allows you to create an SSH tunnel to a running
  Appetize Android session, enabling you to interact with the device via Android
  Studio or standard adb protocol.
---

# ADB tunnel

## Enable ADB Tunnel

To enable the ADB tunnel feature, you can either choose to enable it through a query parameter or by utilizing the JavaScript SDK.

### With Query Parameter

Add the `debug=true` query parameter to your app or embed URL

```uri
&enableAdb=true
```

See [Query Params Reference](../../query-params-reference.md#enableadb) for more information.

### With JavaScript SDK

Set `enableAdb: true` in the configuration e.g.

```typescript
await client.config({
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

The app page provides a simple way to retrieve the `adb` information required to connect to the device. You can access this via your app's app link

{% code overflow="wrap" %}
```url
https://appetize.io/app/{publicKey}?&enableAdb=true
```
{% endcode %}

or by going to your [Apps](https://appetize.io/apps) page, clicking `view` under the app you want to inspect and then toggling `Adb Tunnel` to `On`

<figure><img src="../../../.gitbook/assets/image (10) (1) (1) (5).png" alt="Example App Link with View Action"><figcaption><p>Select "View" under your app</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (2) (1) (1).png" alt="Example ADB Tunnel Action Switched to On"><figcaption><p>Toggle ADB tunnel to "On"</p></figcaption></figure>

Select `Tap To Play` (or your equivalent text to start the session). A command will then be generated that you need to copy and paste in your shell environment e.g.

<figure><img src="../../../.gitbook/assets/image (1) (1) (2) (1).png" alt="Example command to paste in shell environment"><figcaption></figcaption></figure>

Then, the Appetize virtual Android device will appear with `adb devices`, as if it were a device plugged into your computer via USB.

### With JavaScript SDK

You can retrieve all the information needed to start an ADB session via the `getAdbInfo` function

```typescript
const adbInfo = await session.getAdbInfo()
const command = adbInfo.command
```

See our JavaScript [API Reference](../../../javascript-sdk/api-reference.md#getadbinfo) for more information.