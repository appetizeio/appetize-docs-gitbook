---
description: >-
  Easily upload images and other media to your Appetize iOS and Android devices,
  programmatically or via the App Page.
---

# Media

{% hint style="info" %}
The maximum file size for uploading media is **50 MB**.
{% endhint %}

## Supported Files

| Platform | Supported File Types     |
| -------- | ------------------------ |
| Android  | All file types           |
| iOS      | PNG, JPEG, JPG, GIF, MP4 |

{% hint style="warning" %}
Files outside of these formats will not be processed on iOS simulators.
{% endhint %}

The [CLI](../ai-agents/getting-started.md) accepts PNG, JPEG, JPG, GIF and MP4 on both platforms.

## With App Page

The [App Page](../platform/app-management/running-apps.md#accessing-your-app-page) provides an **Upload File** button on the device toolbar during active sessions, allowing you to upload media files directly to the device’s photo library.

<figure><img src="../.gitbook/assets/Screenshot 2025-03-21 114500.png" alt=""><figcaption><p>"Upload File" button during active sessions</p></figcaption></figure>

## With JavaScript SDK

Appetize’s [JavaScript SDK](../javascript-sdk/) offers a convenient [addMedia](../javascript-sdk/api-reference/#addmedia-file) function for adding media files directly to your active simulator sessions. This function is ideal for automating media uploads as part of your testing or development workflows.

```typescript
await session.addMedia(file)
```

## With the CLI

The [CLI](../ai-agents/getting-started.md) adds a photo or video to the device's gallery under its file name:

```bash
appetize media add photo.png
appetize media add ./clips/demo.mp4
```

It prints nothing on success, and fails with the server's message for any other file type or a file over 50 MB.
