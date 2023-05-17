---
description: >-
  Sharing your app on Appetize is easy! Simply upload your build and share the
  link with others for instant access on any device.
---

# Sharing Apps

## Public Key

When you upload an app to Appetize, you receive a link to view your app. This link includes the app's assigned **publicKey**, and looks like this:

```
https://appetize.io/app/:publicKey
```

This **`publicKey`** is an unguessable cryptographically generated 128-bit random string. By default, anybody who has your app's link, i.e. its **publicKey**, will have permission to run your app.

Your app link can be easily shared with whomever you'd like, or [embedded](embedding-apps.md) into your own applications.

{% hint style="info" %}
Some customers want to restrict access, so that only authenticated users may run their app (or certain features). See [App Permissions](app-permissions.md) for more information on how to do this.
{% endhint %}
