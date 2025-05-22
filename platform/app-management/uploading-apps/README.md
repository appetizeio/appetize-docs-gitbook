---
description: >-
  Effortlessly upload your mobile app on Appetize within minutes, and start
  using it across various devices and operating systems.
icon: arrow-up-from-bracket
---

# Uploading Apps

## Preparing your Build

{% content-ref url="android.md" %}
[android.md](android.md)
{% endcontent-ref %}

{% content-ref url="ios.md" %}
[ios.md](ios.md)
{% endcontent-ref %}

{% hint style="info" %}
We support cross-platform apps made in Flutter, Xamarin, React-Native, Kotlin Multiplatform and others which generate`.app` or `.apk` builds.

For common issues and troubleshooting, visit our [Knowledge base](https://support.appetize.io/uploading-and-installing-apps).
{% endhint %}

## Upload your App

### With Upload Page

To upload your application via a web browser use our [Upload](https://appetize.io/upload) dialog:

{% embed url="https://appetize.io/upload" %}

#### Update existing Apps

To update an existing app, follow the same steps as uploading a new app via the [Upload](https://appetize.io/upload) dialog. The [latest build](#user-content-fn-1)[^1] will automatically be associated with your app.

To view all builds for an app, select the app and go to the [App Builds Page](../listing-apps.md#app-builds-page).

{% hint style="warning" %}
In some instances, you might want to explicitly update a particular app build. To do so, follow these steps:

1. Go to the [Apps Dashboard](https://appetize.io/apps).
2. **Select the app**.
3. **Search and select the build** you want to update.
4. Go to **Settings**.
5. Navigate to "**Update build**"

![](<../../../.gitbook/assets/image (4).png>)
{% endhint %}

### With CI/CD and Third-Party Integrations

Appetize integrates with several popular CI/CD tools and other third-party services, allowing you to:

* **Ensure Your App is Always Up-To-Date:**\
  Automatically upload the latest builds with one of our many CI/CD integrations.
* **Eliminate Manual Processes:**\
  Automate rolling out of updated apps or specific builds, saving time and effort.
* **Improve User and Development Workflows:**\
  Integrate with tools such as Storybook Native and Expo to improve user and developer experiences.
* **Run Tests on Pull Requests:**\
  Automatically upload and test builds on Pull Requests for efficient quality assurance.

Available integrations include:

<table data-view="cards"><thead><tr><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden></th><th data-hidden></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td>Github Actions</td><td><a href="https://github.com/appetizeio/github-action-appetize">https://github.com/appetizeio/github-action-appetize</a></td><td></td><td></td><td><a href="../../../.gitbook/assets/github.png">github.png</a></td></tr><tr><td>Gitlab</td><td><a href="https://about.gitlab.com/blog/2020/05/06/how-to-create-review-apps-for-android-with-gitlab-fastlane-and-appetize-dot-io/">https://about.gitlab.com/blog/2020/05/06/how-to-create-review-apps-for-android-with-gitlab-fastlane-and-appetize-dot-io/</a></td><td></td><td></td><td><a href="../../../.gitbook/assets/gitlab.png">gitlab.png</a></td></tr><tr><td>Bitrise</td><td><a href="https://bitrise.io/integrations/steps/appetize-deploy">https://bitrise.io/integrations/steps/appetize-deploy</a></td><td></td><td></td><td><a href="../../../.gitbook/assets/bitrise.png">bitrise.png</a></td></tr><tr><td>Expo</td><td><a href="https://expo.dev/">https://expo.dev/</a></td><td></td><td></td><td><a href="../../../.gitbook/assets/expo.png">expo.png</a></td></tr><tr><td>Fastlane</td><td><a href="https://docs.fastlane.tools/actions/appetize/">https://docs.fastlane.tools/actions/appetize/</a></td><td></td><td></td><td><a href="../../../.gitbook/assets/fastlane.png">fastlane.png</a></td></tr><tr><td>Storybook native</td><td><a href="https://github.com/storybookjs/native">https://github.com/storybookjs/native</a></td><td></td><td></td><td><a href="../../../.gitbook/assets/storybook.png">storybook.png</a></td></tr></tbody></table>

{% hint style="info" %}
If there is a 3rd party integration that you think should be on this list, please let us [know](mailto:support@appetize.io)!
{% endhint %}

### With REST API

Appetize also supports uploading your application programmatically by making use of our [REST API](../../../rest-api/):

{% content-ref url="../../../rest-api/create-new-app.md" %}
[create-new-app.md](../../../rest-api/create-new-app.md)
{% endcontent-ref %}

{% content-ref url="../../../rest-api/update-existing-app.md" %}
[update-existing-app.md](../../../rest-api/update-existing-app.md)
{% endcontent-ref %}

[^1]: The **latest build** refers to the most recent version of your app on Android, identified by the [versionCode](https://developer.android.com/studio/publish/versioning#versioningsettings), and on iOS, by the [CFBundleShortVersionString](https://developer.apple.com/documentation/bundleresources/information_property_list/cfbundleshortversionstring) and [CFBundleVersion](https://developer.apple.com/documentation/bundleresources/information_property_list/cfbundleversion).
