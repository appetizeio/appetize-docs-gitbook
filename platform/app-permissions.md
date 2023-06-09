---
description: >-
  With Appetize's app permissions, users can manage who has access to their app,
  can debug apps or view network traffic logs and more.
---

# App Permissions

## Who can run your app

When you upload an app to Appetize, you receive a link to view your app. This link includes the app's assigned [**publicKey**](sharing-apps.md#public-key), and looks like this:

```
https://appetize.io/app/:publicKey
```

This **`publicKey`** is an unguessable cryptographically generated 128-bit random string. By default, anybody who has your app's link, i.e. its **publicKey**, will have permission to run your app. Your app link can be easily shared with whomever you'd like, or [embedded](embedding-apps.md) into your own applications.

Some customers want to restrict access, so that only authenticated users may run their app. For this purpose, we have a configuration option which can be set at either the app-level or the account-level.

### App Level Permissions

{% hint style="warning" %}
App Level Permissions will override Account Level Permission Defaults
{% endhint %}

For the app-level setting, navigate to your [Dashboard](https://appetize.io/dashboard), then click the "manage" link for your app

<figure><img src="../.gitbook/assets/image (10) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Select "Manage" under your app</p></figcaption></figure>

and finally configure the option under App Permissions.

{% hint style="info" %}
App Level Permissions can also be applied when uploading the app via our REST API. See [Create new app](../rest-api/create-new-app.md) and [Update existing app](../rest-api/update-existing-app.md) for more information.
{% endhint %}

<figure><img src="../.gitbook/assets/image (3) (2).png" alt=""><figcaption><p>Example App Level Permissions</p></figcaption></figure>

### Account Level Permissions

You may also set account-wide permissions on your [Account](https://appetize.io/account).

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p>Example Account Level Permissions</p></figcaption></figure>

## Permissions

Configure the permissions below to determine whether you need to be authenticated to the account or simply have the Embed or View link for an app in order to perform the following actions.

| Permission                | Description                                                          |
| ------------------------- | -------------------------------------------------------------------- |
| **run**                   | Run your application                                                 |
| **networkProxy**          | Specify a network proxy when running the app                         |
| **networkIntercept**      | Use Appetize's intercepting proxy when running the app               |
| **debugLog**              | View your app's NSLog/Logger or Logcat output                        |
| **adbConnect**            | Debug your app by connecting ADB to the hosted emulator              |
| **androidPackageManager** | Allow the installation of additional APK's while your app is running |
