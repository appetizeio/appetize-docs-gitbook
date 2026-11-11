---
description: >-
  Stay updated on Appetize’s latest releases, including new features,
  improvements, and key updates.
icon: paper-plane
layout:
  width: default
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
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
  anchors:
    visible: true
---

# Changelog

## November 2026

### Network Intercept Certificate, Add Media and Automation Updates

* **New Features**
  * New automation commands: terminate an app, wait for the screen to settle before inspecting or taking screenshots, and wait for elements to be checked, disabled, focused or selected
  * Files added with [**Add Media**](https://docs.appetize.io/features/media) now keep their original name
* **Bug Fixes and Improvements**
  * New root certificate for the [**Network Traffic Monitor**](https://docs.appetize.io/features/network-traffic-monitor), trusted on iOS simulators and in Chrome on Android 13–17
  * iOS font size now applies across the whole device, including when changed mid-session

## October 2026

### iOS 27, iPhone 18 Pro and the Foldable iPhone Duo

* **New Features**
  * Added support for **iOS 27** and the **iPhone 18 Pro** and **iPhone 18 Pro Max** devices
  * Added the foldable **iPhone Duo**
    * Fold and unfold the device from the toolbar, or set the starting state with the [`hinge`](https://docs.appetize.io/platform/query-params-reference) parameter
  * [**Device Sandbox**](https://docs.appetize.io/platform/standalone-device) sessions now appear in Session History and usage reports
  * New **Get started** checklist for new users
  * New automation commands for biometrics, app lifecycle (launch, restart, reinstall, clear state), device settings, shake, and screenshots cropped to an element
* **Bug Fixes and Improvements**
  * Clearer app compatibility checks: iOS apps without an ARM build are flagged before the session starts, and the OS picker explains why a device can't run the app
  * Accessibility improvements across the dashboard, including keyboard access, focus styling, labelled form fields and screen-reader-friendly dialogs
  * Password visibility is now always hidden on Android, so the `hidePasswords` parameter is no longer needed and is ignored
  * **iOS 15.5** and **iOS 16.2** have been retired, as they are not supported by the latest Xcode

## September 2026

### International Keyboards and Faster iOS Startup

* **New Features**
  * Characters a US keyboard can't produce (for example Å, Ä and Ö on a Swedish layout) are now typed correctly
  * Set the device [timezone](https://docs.appetize.io/platform/query-params-reference) on iOS
  * New automation commands to open URLs and deep links, clear the keychain, clear app state, and perform custom gestures
* **Bug Fixes and Improvements**
  * Faster iOS session startup

## August 2026

### Session Defaults, Android 17 and Pixel 11

* **New Features**
  * Released the new [**Session Defaults**](https://docs.appetize.io/account/session-defaults) page

    Set organization-wide defaults for devices, behavior, audio, proxy, permissions and session time limits
  * Added support for **Android 17** and the **Pixel 11 Pro** and **Pixel 11 Pro XL** devices
  * [**Access Rules**](https://docs.appetize.io/account/access-rules) now show where each rule applies
  * New automation commands to inspect the view hierarchy, type key sequences, swipe and tap with selectors, and press Android Back. These power the [**Appetize CLI for AI agents**](https://docs.appetize.io/ai-agents)
  * App logs, network capture and the [ADB tunnel](https://docs.appetize.io/features/advanced-features/android/adb-tunnel) can now be turned on mid-session

## July 2026

### Control Where Your Apps Can Be Embedded

* **New Features**
  * Restrict which domains can embed your apps, with blocked embeds recorded in audit events
  * Tap on-screen elements by their text in automation
* **Bug Fixes and Improvements**
  * Supported browsers are now Chrome, Edge and Firefox 111+ and Safari 17+
  * `GET /v2/invite-tokens` no longer returns raw tokens. Delete invites with `DELETE /v2/invite-tokens/{username}`

## June 2026

### Embed Sign-In and Security Improvements

* **Bug Fixes and Improvements**
  * Signing in from an embed now works when the browser blocks third-party cookies
  * Changing your password now signs you out of your other sessions
  * Server-side MP4 screen recording and the `screenRecording` session option have been removed

## May 2026

### Audio Streaming for Android

* **New Features**
  * Added [**audio streaming**](https://docs.appetize.io/features/audio) for Android sessions, toggled from the configuration menu or with `?audio=true`

## April 2026

### Custom Branding and Live Appearance Switching

* **New Features**
  * New [**Custom Branding**](https://docs.appetize.io/features/custom-branding) section in Organization Settings
  * Switch between light and dark appearance during a session
  * Set the device [timezone](https://docs.appetize.io/platform/query-params-reference) on Android
  * The build view now shows file size and code signatures
* **Bug Fixes and Improvements**
  * Clearer error messages when an app fails to install

## March 2026

### Frame Rate Control and Better Keyboard Input

* **New Features**
  * Set the session frame rate at launch
  * Support for composed key input, such as accented characters typed with dead keys
  * Disable built-in apps on Android
* **Bug Fixes and Improvements**
  * iOS deep links are trusted automatically when `grantPermissions` is set

## February 2026

### Font Size Control and Android Immersive Mode

* **New Features**
  * Set the device font size at launch or during a session, on both iOS and Android
  * Android immersive mode and auto-rotate support
  * Set app permissions without launching the app
* **Bug Fixes and Improvements**
  * Higher v2 API rate limits

## November 2025

### **New API Token Management Page**

<figure><img src=".gitbook/assets/image (79).png" alt=""><figcaption><p>New API Token Management Page</p></figcaption></figure>

* **New Features**
  *   Released the new [**API Token Management**](https://appetize.io/organization/api-tokens) page

      Create, revoke, and manage API tokens directly from your dashboard\
      [View documentation](https://docs.appetize.io/account/api-tokens)
  * Added **Shake Device** button to the toolbar for Android apps
* **Bug Fixes and Improvements**
  * Improved **Billing page** to show all invoices including their statuses
  * Fixed issue where app groups sometimes selected the wrong build when the same `appId` was used across platforms
  * Improved file download names for network and debug logs
  * Resolved errors when dragging non-files onto the upload area
  * Fixed session invite behavior and role handling when re-inviting users
  * Show tooltip when session history username gets clipped

## September 2025

### iOS 26, iPhone 17 Support, and a New Automation Engine

<figure><img src=".gitbook/assets/image (77).png" alt="iOS 26 &#x26; iPhone 17 devices added"><figcaption><p>iOS 26 &#x26; iPhone 17 devices added</p></figcaption></figure>

* **New Features**
  * Added support for **iOS 26** and the latest **iPhone 17** and **iPhone 17 Pro Max** devices
  *   Launched a new **automation engine**

      * Faster, more reliable, and built to support modern declarative frameworks like SwiftUI, Compose, Flutter and more.
      * The new engine is **more integrated with the Appetize platform**, laying the groundwork for richer automation features ahead.

      [Read the announcement](https://appetize.io/blog/posts/introducing-our-new-automation-engine)
* **Bug Fixes and Improvements**
  * Added **"All iOS"** and **"All Android"** filters to easily explore sessions across entire platforms
  * Updated the **App Page** for anonymous users to match the styling of logged-in views
  * Improved support for **split APK installations** across Android devices
  * Fixed SSO configuration issues and improved fallback when multiple strategies are in use
  * Android app metadata now includes signing information for better visibility

## August 2025

### Session History View and Android 16 Support

<figure><img src=".gitbook/assets/image (76).png" alt="Picture of the new Session History View"><figcaption><p>New Session History View</p></figcaption></figure>

* **New Features**
  * Released the new [**Session History**](https://appetize.io/sessions) view
    * Easily view, search and export previous sessions to help with debugging, tracking activity, and understanding recent usage across your team.
  * Added support for **Android 16** and **Pixel 9 devices**
    * Ensures compatibility with the latest Android OS and new device models
* **Bug Fixes and Improvements**
  * Added support for **split APKs** (including non-Bundletool) build variants.
  * Redesigned the **Build Metadata** page for clearer app build details.
  * Added **syntax highlighting** to debug logs for easier reading and troubleshooting
  * Enabled **S3 Transfer Acceleration** to speed up file uploads and downloads in supported regions
  * Added **version-based search** in the Builds view
  * Increased screenshot timeout to 60 seconds for better reliability on slower or complex apps
  * Extended accepted file types for uploads on both iOS and Android devices
  * Fixed session parameters not being saved properly
  * Improved error handling for SSO logins and duplicate email invitations
  * Resolved issues with tooltips causing duplicate clicks
  * Improved OIDC login flow, including **support for Amazon Cognito**
  * Fixed device OS selection and APK parsing issues during app installs
  * Fixed layout bugs in debug logs, toolbars, and developer settings
  * Persisted sidebar drawer state using cookies
  * Improved pointer accuracy in the Inspector tool when overlapping UI elements are present

## May 2025

### Improved User Invitation Journey & Easier API Access

<figure><img src=".gitbook/assets/Changelog Update - Invites.jpg" alt="New User Invitation Journey"><figcaption><p>New User Invitation Journey</p></figcaption></figure>

* **New Features**
  * Introduced a [new **user invitation journey**](https://docs.appetize.io/account/invite-your-team) with predefined roles and better onboarding experience.
  * Added support for the `x-api-key` header in both v1 and v2 API authentication.
  * Enabled linking to **external launch pages** from within the Appetize App Experience.
  * Added **Pixel Tablet** to supported devices.
* **Bug Fixes and Improvements**
  * Fixed crash caused by unsafe `endSession` calls during app downloads
  * Resolved APK reinstall and upload issues
  * Improved Android emulator performance
  * Fixed memory issues caused by large app aggregations
  * Corrected issues with `lastPlayed` property updates
  * Improved iOS architecture metadata display
  * Updated email styling and fixed layout issues across login, signup, and developer tools UI

## March 2025

### Redesigned App Experience

<figure><img src=".gitbook/assets/Changelog Update 2028.jpg" alt=""><figcaption><p>Updated App Page Experience</p></figcaption></figure>

* **New Features:**
  * Web app redesign
    * The app page now includes a new toolbar for faster access to often used actions such as taking screenshots, biometric data, changing location and much more!
    * Refreshed visual design across all pages for a more consistent and intuitive experience.
  * Introduced `launchApp` parameter
    * Indicates whether an app should launch after installation, and allows specifying which installed app to open automatically.
  * Broadened device support with new Pixel 9 options and enhanced custom device configuration.
* **Bug Fixes and Improvements:**
  * Improved Android 15 support with enhancements to language changes, proxy behaviour, and general reliability.
  * Enabled Android emulators to unlock extended host CPU features.
  * Upgraded iOS runtime support to version 18.2
  * Resolved session stability issues in app groups and improved build resolution accuracy.
  * Improved UI consistency with improvements to buttons, layout spacing, tab behaviour, and component styling.
  * Strengthened federated login flows with better handling of missing user details and stricter redirect validation.
  * Corrected device-specific behaviour such as toolbar spacing and biometric icon rendering on older iOS devices.

## December 2024

### Android 15 Support

<figure><img src=".gitbook/assets/Android 15.png" alt=""><figcaption><p>Android 15 Support</p></figcaption></figure>

* **New Features:**
  * Support for **Android 15** on newer devices.
  * Support for multiple iOS keyboards, now configurable as an array.
  * Added **build.maxConcurrent** for enhanced concurrency management.
* **Bug Fixes and Improvements:**
  * Expanded [v1 API](https://docs.appetize.io/rest-api/create-new-app) to support additional fields:
    * `timeLimit`
    * `maxConcurrent`
    * `referrerHostnamesRestricted`
  * Android back camera now defaults to virtual scene on newer OS Versions.
  * Improved localization and framework parsing logic for iOS.
  * Fixed incorrect handling of `shiftKey` values during keypress events.
  * Resolved Android loopback issues and enhanced HTTP redirector functionality.
  * Prevented default behavior for `cmd/ctrl + K` to avoid conflicts.

## November 2024

### iOS 18 & iPhone 16 Pro/Max Support

<figure><img src=".gitbook/assets/product-devices-noround.png" alt=""><figcaption><p>iOS 18 and iPhone 16 Pro/Max support has been added</p></figcaption></figure>

* **New Features**:
  * Support for **iOS 18** and **iPhone 16** **Pro/Max** devices.
  * Improved **Organization Settings** UI with clearer section names and options.
  * **Stripe** checkout flow added for credit card updates.
  * Updated default devices to **iPhone 14 Pro** and **Pixel 7**.
* **Bug fixes & Improvements**:
  * Fixed **video rotation** issues on Chrome 130.
  * Fixed session parameters and **configuration** handling in consecutive sessions.
  * Improved **login** redirects and federated login flow.
  * Addressed **duplicate invite token** for registered users.
  * Improved clarity for overage charges and invoice details.
  * Improved **@appetize/create-playwright** template & intro messaging.
  * **Android 5-7** have been retired due to their age and limited usage, allowing us to focus on improving compatibility with modern devices.

## October 2024

### Biometry Support for iOS, JS SDK Updates & Other Improvements

<figure><img src=".gitbook/assets/biometrics (1).png" alt=""><figcaption><p>We now support Biometry features on both iOS and Android</p></figcaption></figure>

* **New Features**:
  * Added [biometry support](https://docs.appetize.io/javascript-sdk/automation/device-commands#biometry) for iOS.
  * Improved SDK action titles in Playwright trace sidebar.
  * Support for Google and Github Login Providers.
* **Bug fixes & Improvements**:
  * Faster build ID validation.
  * [ADB Tunnel](https://docs.appetize.io/features/advanced-features/android/adb-tunnel) can now be used for sessions using [AppRecorder](/broken/pages/Gm30V6WlKjLSc4ey0eXF), network proxies, and debug logs
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

### New App Dashboard

<figure><img src=".gitbook/assets/image (74).png" alt="New App Dashboard: Streamlined to find the right apps faster"><figcaption><p>New App Dashboard: Streamlined to find the right apps faster</p></figcaption></figure>

* **Enhanced App Organization**:\
  Apps are now organized by their unique application identifier. See our [App Dashboard documentation](https://docs.appetize.io/platform/app-management/listing-apps) for more info.
* **Simplified App Group Management**:\
  Easier creation and management of App Groups, with options to always use the latest build.
* **Improved Dashboard Performance**:\
  Faster load times and responsiveness, paving the way for future features.
* **Upcoming Features**:\
  Look forward to more API versatility, granular management options, and new UI automation tools.

For more information, see our [blog post](https://appetize.io/posts/updates/2024/07/03/new-app-dashboard-streamlined-to-find-the-right-apps-faster).
