---
description: >-
  Get a quick preview and seamless experience of your app across multiple
  devices and operating systems with Appetize's user-friendly App page.
icon: play
---

# Running Apps

## Features

<figure><img src="../../.gitbook/assets/Screenshot 2023-10-24 114520.png" alt=""><figcaption><p>App Page</p></figcaption></figure>

Appetize provides an out-of-the-box App page that provides easy access to:

* Different Supported [Devices and OS Versions](../../features/devices-and-os-versions.md).
* Debugging features:
  * [UI Automation (AppRecorder)](../../features/ui-automation.md)
  * [Network Traffic Monitor](../../features/network-traffic-monitor.md)
  * [Debug Logs](../../features/debug-logs.md)
  * [Adb Tunnel](../../features/advanced-features/android/adb-tunnel.md) (Android Only)
* Adding Media
* Saving screenshots
* Support for all [Query Parameters](../query-params-reference.md) to fully customize your experience.

<figure><img src="../../.gitbook/assets/Screenshot 2023-10-24 115356.png" alt="" width="221"><figcaption><p>Easily switch devices, enable debugging features, save screenshots and more.</p></figcaption></figure>

## Accessing your App Page

#### Latest Build

You can access the latest build associated with your app by making use of your app identifier and platform in the URL e.g.

{% code overflow="wrap" %}
```url
https://appetize.io/apps/{platform}/{appId}
```
{% endcode %}

Alternatively you can go to  your [Apps](https://appetize.io/apps) page and click **play** on the app you want to run.

#### Specific Build

You can access a specific build of your app by making use of your buildId (or previously known as publicKey) in the URL e.g.

```
https://appetize.io/app/{buildId}
```

{% hint style="info" %}
If you are still using our v1 API, the buildId and the publicKey will be interchangeable e.g.

```
https://appetize.io/app/{publicKey|buildId}
```
{% endhint %}

Alternatively you can go to  your [Apps](https://appetize.io/apps) page and select the App with which the build is associated. From here you can access the individual builds as explained [here](listing-apps.md#app-builds-page). &#x20;
