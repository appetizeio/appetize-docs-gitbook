---
description: Effortlessly run your app on a diverse range of devices and operating systems
---

# Devices & OS Versions

Appetize strive to support a healthy mixture of Android emulators and iOS simulators in order for you to get the most out of our product.

{% hint style="info" %}
We understand that every business has unique needs and that's why we also offer customized configurations and devices through our Private Cloud offerings. [Contact us](https://appetize.io/contact-us) to learn more.
{% endhint %}

## Supported Devices

| Device                        | Device Identifier           | Operating System Versions           |
| ----------------------------- | --------------------------- | ----------------------------------- |
| **iOS**                       |                             |                                     |
| iPhone 8                      | iphone8                     | 14.5, 15.5, 16.2                    |
| iPhone 8 Plus                 | iphone8plus                 | 14.5, 15.5, 16.2                    |
| iPhone 11 Pro                 | iphone11pro                 | 14.5, 15.5, 16.2, 17.0              |
| iPhone 12                     | iphone12                    | 14.5, 15.5, 16.2, 17.0              |
| iPhone 13 Pro                 | iphone13pro                 | 15.5, 16.2, 17.0                    |
| iPhone 13 Pro Max             | iphone13promax              | 15.5, 16.2, 17.0                    |
| iPhone 14 Pro                 | iphone14pro                 | 16.2, 17.0                          |
| iPhone 14 Pro Max             | iphone14promax              | 16.2, 17.0                          |
| iPhone 15 Pro                 | iphone15pro                 | 17.0                                |
| iPhone 15 Pro Max             | iphone15promax              | 17.0                                |
| iPad Air 4th generation       | ipadair4thgeneration        | 14.5, 15.5, 16.2, 17.0              |
| iPad Pro 12.9" 5th generation | ipadpro129inch5thgeneration | 14.5, 15.5, 16.2, 17.0              |
| iPad 9th generation           | ipad9thgeneration           | 15.5, 16.2, 17.0                    |
|                               |                             |                                     |
| **Android**                   |                             |                                     |
| Nexus 5                       | nexus5                      | 5.1, 6.0, 7.1, 8.1, 9.0, 10.0, 11.0 |
| Pixel 4                       | pixel4                      | 10.0, 11.0, 12.0                    |
| Pixel 4 XL                    | pixel4xl                    | 10.0, 11.0, 12.0                    |
| Pixel 6                       | pixel6                      | 12.0, 13.0                          |
| Pixel 6 Pro                   | pixel6pro                   | 12.0, 13.0                          |
| Pixel 7                       | pixel7                      | 13.0                                |
| Pixel 7 Pro                   | pixel7pro                   | 13.0                                |
| Galaxy Tab S7                 | galaxytabs7                 | 10.0, 11.0, 12.0, 13.0              |

{% hint style="info" %}
For devices utilizing a PIN/Lock Screen, our default PIN code is set to **1111** for seamless access and testing.
{% endhint %}

A dynamic, up-to-date list of all the devices and operating systems we support can be retrieved via our REST API

{% content-ref url="../rest-api/devices-and-os-versions.md" %}
[devices-and-os-versions.md](../rest-api/devices-and-os-versions.md)
{% endcontent-ref %}

## Usage

{% hint style="warning" %}
Usage in our JavaScript SDK or query parameters require the device identifier e.g. `iphone8plus` or `ipadair4thgeneration`
{% endhint %}

### With Query Parameters

Set the device type and Operating System version by adding the `device` and/or `osVersion` query parameter to your app or embed URL.

```uri
&device=pixel4&osVersion=12.0
```

See [Query Params Reference](query-params-reference.md#device) for more information.

### With JavaScript SDK

Set the device type and Operating System version by adding the `device` and/or `osVersion` properties during configuration.

```typescript
await client.config({
    device: 'pixel4',
    osVersion: '12.0'
})
```

See [Configuration](../javascript-sdk/configuration.md#device) for more information.
