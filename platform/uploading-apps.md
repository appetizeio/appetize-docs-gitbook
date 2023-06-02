---
description: >-
  Effortlessly upload your mobile app on Appetize within minutes, and start
  using it across various devices and operating systems.
---

# Uploading Apps

## Preparing your Build

{% content-ref url="uploading-apps/android.md" %}
[android.md](uploading-apps/android.md)
{% endcontent-ref %}

{% content-ref url="uploading-apps/ios.md" %}
[ios.md](uploading-apps/ios.md)
{% endcontent-ref %}

{% hint style="info" %}
We also support apps made in Flutter, Xamarin, React-Native, Kotlin Multiplatform and other similar cross-platform environments, as long as the resulting `.app` or `.apk` build is generated.

If you are experiencing any issues, please see our [Knowledge base](https://support.appetize.io/uploading-and-installing-apps) for more information.
{% endhint %}

## Uploading your App

### With Upload Page

You can upload your application directly via a web browser by making use of our [Upload](https://appetize.io/upload) page:

{% embed url="https://appetize.io/upload" %}

{% hint style="info" %}
If you have an existing app that you would like to update, you can upload a new build within the manage page of that app. Select `manage` under the app listed in your [Apps Dashboard](https://appetize.io/apps) and navigate to `Upload a new build`.

<img src="../.gitbook/assets/image (10) (1) (1) (3).png" alt="Example App with Manage action" data-size="original">
{% endhint %}

### With REST API

Appetize also supports uploading your application programmatically by making use of our [REST API](broken-reference/):

{% content-ref url="../rest-api/create-new-app.md" %}
[create-new-app.md](../rest-api/create-new-app.md)
{% endcontent-ref %}

{% content-ref url="../rest-api/update-existing-app.md" %}
[update-existing-app.md](../rest-api/update-existing-app.md)
{% endcontent-ref %}

### With 3rd Party Integrations

Appetize has several 3rd party integrations for popular tools to allow you to quickly upload your application:

* [Fastlane](https://docs.fastlane.tools/actions/appetize/)
* [Bitrise](https://bitrise.io/integrations/steps/appetize-deploy)
* [Github Actions](https://github.com/appetizeio/github-action-appetize)
* [Expo](https://expo.dev/)
* [Storybook Native](https://github.com/storybookjs/native)

{% hint style="info" %}
If there is a 3rd party integration that you think should be on this list, please let us [know](mailto:support@appetize.io)!
{% endhint %}
