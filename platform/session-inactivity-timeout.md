---
icon: alarm-clock
description: >-
  With Appetize's Session Inactivity Timeout, users can manage how long their
  device's session stays active, before being freed up for reuse.
---

# Session Inactivity Timeout

By **default**, your Appetize session will end after **2 minutes** of inactivity. You can modify the default app timeout, or specify a timeout for a specific app build by following the steps below:

## Default App Timeout

Navigate to [**Organization -> Apps**](https://appetize.io/organization/apps) **->** **Session Timeout**

<figure><img src="../.gitbook/assets/image (53).png" alt="" width="395"><figcaption><p>Default App Session Timeout</p></figcaption></figure>

## App Build Specific Timeout

Navigate to your [**Apps Dashboard**](https://appetize.io/apps) **-> Select** your preferred **app -> Select the build** you want to modify **-> Settings ->  Session timeout**

<figure><img src="../.gitbook/assets/image (43).png" alt="" width="372"><figcaption><p>Select the App you want to modify</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (44).png" alt=""><figcaption><p>Select the build you want to modify</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (45).png" alt=""><figcaption><p>Build Specific Inactivity Timeout</p></figcaption></figure>



{% hint style="info" %}
You can also[ set](../rest-api/create-new-app.md)/[update](../rest-api/update-existing-app.md) the inactivity timeout of your app with our [REST API](../rest-api/) when uploading your app.
{% endhint %}

## What's the behavior if you reach your concurrency limit?

When a user launches Appetize and the maximum concurrency limit has been reached, they will be placed in a virtual 'queue' and wait until additional capacity becomes available:

<figure><img src="../.gitbook/assets/image (3).png" alt="" width="360"><figcaption><p>Sample of reaching the concurrency queue in our demo experience</p></figcaption></figure>

As soon as a device becomes available, the queued users will be granted access, allowing them to continue as usual.
