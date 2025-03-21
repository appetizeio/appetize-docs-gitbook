---
description: >-
  Sharing your app on Appetize is easy! Simply upload your build and share the
  link with others for instant access on any device.
icon: share-nodes
---

# Sharing

## Where is my share link?

The easiest way to find your external share link is by going to your [Apps](https://appetize.io/apps) or [App Builds](app-management/listing-apps.md#app-builds-page) page and selecting **share** under the app, App Group or build that you want to embed on your website.

<figure><img src="../.gitbook/assets/Screenshot 2025-03-21 113309.png" alt=""><figcaption><p>Find your share link by clicking the share button</p></figcaption></figure>

Currently, `Share` will share a specific build of your application. Soon, we will introduce new sharing features that will allow you to share the latest build without changing the URL.

<figure><img src="../.gitbook/assets/image (19).png" alt="" width="386"><figcaption><p>Example Share dialog</p></figcaption></figure>

## App Identifier

App builds hosted on Appetize are distinguished by their unique Application Identifier. On Android, this identifier corresponds to the [Application ID](https://developer.android.com/build/configure-app-module#set-application-id), while on iOS, it is known as the [Bundle Identifier](https://developer.apple.com/documentation/appstoreconnectapi/bundle_ids).

You can access the [latest build](#user-content-fn-1)[^1] of a particular application like this:

```
https://appetize.io/apps/{platform}/{appId}
```

{% hint style="warning" %}
By default, only users linked to your organization and signed in to Appetize will have access to your App Identifier link.
{% endhint %}

This link can also be further filtered to a specific type of build by passing in the preferred metadata e.g.

* By tag `https://appetize.io/apps/{platform}/{appId}?tag=dev`
* By version `https://appetize.io/apps/{platform}/{appId}/{versionName}`

## Build Identifier

_Previously known as publicKey_

When you upload an app build to Appetize, you receive a link to view your app. This link includes the app's assigned **buildId**, and looks like this:

```
https://appetize.io/app/{buildId}
```

By default, anybody who has your app's build link, i.e. its **buildId** (previously known as **publicKey**), will have permission to run your app.

Your app link can be easily shared with whomever you'd like, or [embedded](embedding-apps.md) into your own applications.

{% hint style="info" %}
Some customers want to restrict access, so that only authenticated users may run their app (or certain features). See [App Build Permissions](app-management/app-permissions.md) for more information on how to do this.
{% endhint %}

[^1]: The **latest build** refers to the most recent version of your app on Android, identified by the [versionCode](https://developer.android.com/studio/publish/versioning#versioningsettings) , and on iOS, by the [CFBundleShortVersionString](https://developer.apple.com/documentation/bundleresources/information_property_list/cfbundleshortversionstring) and [CFBundleVersion](https://developer.apple.com/documentation/bundleresources/information_property_list/cfbundleversion).
