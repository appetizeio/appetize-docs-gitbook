---
icon: paper-plane
description: >-
  Stay updated on Appetize’s latest releases, including new features,
  improvements, and key updates.
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
---

# Changelog

## November 2024

### iOS 18 & iPhone 16 Pro/Max Support

<figure><img src=".gitbook/assets/ios18.png" alt=""><figcaption><p>iOS 18 and iPhone 16 Pro/Max support has been added</p></figcaption></figure>

* **New Features**:&#x20;
  * Support for **iOS 18** and **iPhone 16** **Pro/Max** devices.
  * Improved **Organization Settings** UI with clearer section names and options.
  * **Stripe** checkout flow added for credit card updates.
  * Updated default devices to **iPhone 14 Pro** and **Pixel 7**.
* **Bug fixes & Improvements**:&#x20;
  * Fixed **video rotation** issues on Chrome 130.
  * Fixed session parameters and **configuration** handling in consecutive sessions.
  * Improved **login** redirects and federated login flow.
  * Addressed **duplicate invite token** for registered users.
  * Improved clarity for overage charges and invoice details.
  * Improved **@appetize/create-playwright** template & intro messaging.
  * **Android 5-7** has been retired due to their age and limited usage, allowing us to focus on improving compatibility with modern devices.

## October 2024

### Biometry Support for iOS, JS SDK Updates & Other Improvements

<figure><img src=".gitbook/assets/biometrics (1).png" alt=""><figcaption><p>We now support Biometry features on both iOS and Android</p></figcaption></figure>

* **New Features**:&#x20;
  * Added [biometry support](https://docs.appetize.io/javascript-sdk/automation/device-commands#biometry) for iOS.
  * Improved SDK action titles in Playwright trace sidebar.
  * Support for Google and Github Login Providers.
* **Bug fixes & Improvements**:&#x20;
  * Faster build ID validation.
  * &#x20;[ADB Tunnel](https://docs.appetize.io/features/advanced-features/android/adb-tunnel) can now be used for sessions using [AppRecorder](features/ui-automation.md), network proxies, and debug logs
  * Debug log and session info attached to test results.
  * Playwright peer dependency upgrade.
  * Fixed issue where `startSession` was not throwing errors on `userError`.
  * Resolved incorrect aliasing of `publicKey` in `EmbedWindow` class.
  * Prevented no-op on `restartApp` and `reinstallApp` for standalone session.
  * Improvements to `setLanguage` to ensure its more reliable.
  * Support for WebView scaling on iOS.
  * Improvements to Universal Link validation process.
  * Fix corrupted [Intercept proxy](https://docs.appetize.io/features/network-traffic-monitor) responses when chunked transfer encoding is used.

## July 2024

### New App Dashboard&#x20;

<figure><img src=".gitbook/assets/image (67).png" alt="New App Dashboard: Streamlined to find the right apps faster"><figcaption><p>New App Dashboard: Streamlined to find the right apps faster</p></figcaption></figure>

* **Enhanced App Organization**: \
  Apps are now organized by their unique application identifier. See our [App Dashboard documentation](https://docs.appetize.io/platform/app-management/listing-apps) for more info.
* **Simplified App Group Management**: \
  Easier creation and management of App Groups, with options to always use the latest build.
* **Improved Dashboard Performance**: \
  Faster load times and responsiveness, paving the way for future features.
* **Upcoming Features**: \
  Look forward to more API versatility, granular management options, and new UI automation tools.

For more information, see our [blog post](https://appetize.io/posts/updates/2024/07/03/new-app-dashboard-streamlined-to-find-the-right-apps-faster).
