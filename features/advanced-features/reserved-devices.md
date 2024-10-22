---
description: >-
  Ensure lightning-fast loading times for commonly used apps by keeping them
  ready to go on reserved devices.
---

# Reserved Devices

{% hint style="info" %}
This feature is only available on our Premium and Enterprise plans. [Contact us](https://appetize.io/contact-us) to learn more.
{% endhint %}

With reserved devices, Appetize will pre-install your specified apps onto a set of virtual devices. These devices are set aside for solely your use.

When an incoming session is requested for your app, the session can be served from one of these reserved devices, and loads nearly instantaneously for you user. The user does not need to wait for the download and installation of your app, or in rare cases needing to switch the device if the requested device is unavailable. Loading time is extremely fast.

### Requesting Reserved Devices

To request a reserved device through Appetize, you need to provide specific information.

* **buildId:** Application build identifier (previously known as publicKey).
* **deviceType:** The device that is going to be reserved. e.g., iphone14pro.
* **OSVersion:** The operating system version for the device. e.g., 17.2.

See [Devices & OS Versions](../devices-and-os-versions.md) for possible device combinations.

### Accessing your Reserved Device

Once your reserved device has been configured and is ready for use, you can access it through the following URL:

Replace the **buildId**, **deviceType**, and **OSVersion** placeholders with the values provided.

{% code overflow="wrap" %}
```
https://appetize.io/app/{buildId}?device={deviceType}&osVersion={OSVersion}
```
{% endcode %}
