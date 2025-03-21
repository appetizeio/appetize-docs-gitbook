---
description: >-
  With Appetize's app permissions, users can manage who has access to their app,
  can debug apps or view network traffic logs and more.
icon: key
---

# App Permissions

## Who can run your app

### App Identifier Link

See Sharing [**App Identifier Links**](../sharing-apps.md#app-identifier).

By default, only users linked to your organization and signed in to Appetize will have access to your App Identifier link.

### Build Identifier Link

See Sharing [**Build Identifier Links**](../sharing-apps.md#build-identifier).

By default, anybody who has your app's Build Identifier link, i.e. its **buildId** (previously known as **publicKey**), will have permission to run your app.

Some customers want to restrict access, so that only authenticated users may run their app. For this purpose, we have a configuration option which can be set at either the organization level or the app build level.

## Organization Session Default Permissions

Set and control default session permissions across your organization by navigating to [**Organization -> Session Defaults**](https://appetize.io/organization/session-defaults).

<figure><img src="../../.gitbook/assets/Screenshot 2025-03-21 112952.png" alt=""><figcaption><p>Example Organization App Build Permissions</p></figcaption></figure>

## App Build Permissions

{% hint style="warning" %}
App Build Permissions will override Organization Session Default Permissions. We recommend using Organization Session Default Permissions. In the future we will introduce more granular ways to provide permissions for your apps.
{% endhint %}

For the app-level setting, navigate to your [**Dashboard**](https://appetize.io/dashboard), select your preferred app and then select the build you want to change permissions for:

<figure><img src="../../.gitbook/assets/Screenshot 2025-03-21 113201.png" alt=""><figcaption><p>Select the build you want to apply permission to</p></figcaption></figure>

and finally configure the option under Settings > App Permissions.

{% hint style="info" %}
App Level Permissions can also be applied when uploading the app via our REST API. See [Create new app](../../rest-api/create-new-app.md) and [Update existing app](../../rest-api/update-existing-app.md) for more information.
{% endhint %}

<figure><img src="../../.gitbook/assets/Screenshot 2025-03-21 113050.png" alt=""><figcaption><p>Example App Build Level Permissions</p></figcaption></figure>

## Permissions

Configure the permissions below to determine whether you need to be authenticated with Appetize and linked to the organization or simply have the Embed or View link for an app in order to perform the following actions.

| Permission                | Description                                                          |
| ------------------------- | -------------------------------------------------------------------- |
| **run**                   | Run your application                                                 |
| **networkProxy**          | Specify a network proxy when running the app                         |
| **networkIntercept**      | Use Appetize's intercepting proxy when running the app               |
| **debugLog**              | View your app's NSLog/Logger or Logcat output                        |
| **adbConnect**            | Debug your app by connecting ADB to the hosted emulator              |
| **androidPackageManager** | Allow the installation of additional APK's while your app is running |
