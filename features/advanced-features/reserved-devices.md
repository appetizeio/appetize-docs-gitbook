---
description: >-
  Ensure lightning-fast loading times for commonly used apps by keeping them
  ready to go on reserved devices.
---

# Reserved Devices

{% hint style="info" %}
This feature is only available on our Premium and Enterprise plans. [Contact us](https://appetize.io/contact-us) to learn more.
{% endhint %}

With reserved devices, Appetize will pre-install your specified apps onto a set of virtual devices. These devices are set aside for solely your use.&#x20;

When an incoming session is requested for your app, the session can be served from one of these reserved devices, and loads nearly instantaneously for you user. The user does not need to wait for the download and installation of your app, or in rare cases needing to switch the device if the requested device is unavailable. Loading time is extremely fast.&#x20;

### Requesting Reserved Devices

When requesting reserved devices, please share the specific app link you would like reserved. The app link will include the **publicKey** for the app, as well as the **specific device type** and **operating system version**.&#x20;

{% code overflow="wrap" %}
```
https://appetize.io/app/{publicKey}?device={deviceType}&osVersion={OSVersion}
```
{% endcode %}

See [Devices & OS Versions](../devices-and-os-versions.md) for possible device combinations.
