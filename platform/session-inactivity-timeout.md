---
description: >-
  With Appetize's session inactivity timeout, users can manage how long their
  device's session stays active, before being freed up for reuse.
---

# Session Inactivity Timeout

By **default**, your Appetize session will end after **2 minutes** of inactivity. You can modify the default app timeout, or specify a timeout for a specific app by following the steps below:

## Default App Timeout

Navigate to your [**Account Dashboard**](https://appetize.io/account) **->** **Default app settings** -> **Default inactivity timeout**

<figure><img src="../.gitbook/assets/image (1) (2).png" alt="" width="563"><figcaption><p>Default App Inactivity Timeout</p></figcaption></figure>

## App Specific Timeout

Navigate to your [**App Dashboard**](https://appetize.io/apps) **-> Manage** (under your preferred app) **-> Session timeout**

<figure><img src="../.gitbook/assets/image (10) (1) (1) (1) (1) (5).png" alt="" width="366"><figcaption><p>Select "manage" under your preferred app</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (8).png" alt="" width="455"><figcaption><p>App specific Inactivity Timeout</p></figcaption></figure>

{% hint style="info" %}
You can also[ set](../rest-api/create-new-app.md)/[update](../rest-api/update-existing-app.md) the inactivity timeout of your app with our [REST API](broken-reference) when uploading your app.
{% endhint %}

## What's the behavior if you reach your concurrency limit?

When a user launches Appetize and the maximum concurrency limit has been reached, they will be placed in a virtual 'queue' and wait until additional capacity becomes available:

<figure><img src="../.gitbook/assets/image (3).png" alt="" width="360"><figcaption><p>Sample of reaching the concurrency queue in our demo experience</p></figcaption></figure>

As soon as a device becomes available, the queued users will be granted access, allowing them to continue as usual.
