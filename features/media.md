---
description: >-
  Easily upload images and other media to your Appetize iOS and Android devices,
  programmatically or via the App Page.
---

# Media

{% hint style="info" %}
The maximum file size for uploading media is **50 MB**.
{% endhint %}

## With App Page

The [App Page](../platform/app-management/running-apps.md#accessing-your-app-page) provides an **Add Media** button during active sessions, allowing you to upload media files directly to the device’s photo library.

<figure><img src="../.gitbook/assets/image (68).png" alt="" width="221"><figcaption><p>"Add Media" button during active sessions</p></figcaption></figure>

## With JavaScript SDK

Appetize’s [JavaScript SDK](../javascript-sdk/) offers a convenient [addMedia](../javascript-sdk/api-reference.md#addmedia-file) function for adding media files directly to your active simulator sessions. This function is ideal for automating media uploads as part of your testing or development workflows.

```typescript
await session.addMedia(file)
```
