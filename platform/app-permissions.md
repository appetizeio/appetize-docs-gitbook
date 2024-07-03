---
description: >-
  With Appetize's app permissions, users can manage who has access to their app,
  can debug apps or view network traffic logs and more.
---

# App Permissions

## Who can run your app

### App Identifier Link

See Sharing [App Identifier Links](sharing-apps.md#app-identifier).

By default, only users signed in to your account will have access to your App Identifier link.

### Build Identifier Link

See Sharing [Build Identifier Links](sharing-apps.md#build-identifier).

By default, anybody who has your app's Build Identifier link, i.e. its **buildId** (previously known as **publicKey**), will have permission to run your app.

Some customers want to restrict access, so that only authenticated users may run their app. For this purpose, we have a configuration option which can be set at either the account-level or the app-build-level.

## Account Level Permissions

You can apply account-wide permissions on your [Account](https://appetize.io/account).

<figure><img src="../.gitbook/assets/image (1) (1) (3).png" alt=""><figcaption><p>Example Account Level Permissions</p></figcaption></figure>

## App Build Level Permissions

{% hint style="warning" %}
App Build Level Permissions will override Account Level Permission Defaults. We recommend using Account Level Defaults. In the future we will introduce more granular ways to provide permissions for your apps.
{% endhint %}

For the app-level setting, navigate to your [Dashboard](https://appetize.io/dashboard), select your preferred app and then select the build you want to change permissions for:

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption><p>Select the build you want to apply permission to</p></figcaption></figure>

and finally configure the option under Settings >  App Permissions.

{% hint style="info" %}
App Level Permissions can also be applied when uploading the app via our REST API. See [Create new app](../rest-api/create-new-app.md) and [Update existing app](../rest-api/update-existing-app.md) for more information.
{% endhint %}

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption><p>Example App Build Level Permissions</p></figcaption></figure>

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
