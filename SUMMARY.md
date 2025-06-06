# Table of contents

* [Introduction](README.md)
* [Platform](platform/README.md)
  * [App Management](platform/app-management/README.md)
    * [Uploading Apps](platform/app-management/uploading-apps/README.md)
      * [Android](platform/app-management/uploading-apps/android.md)
      * [iOS](platform/app-management/uploading-apps/ios.md)
    * [App Dashboard](platform/app-management/listing-apps.md)
    * [Running Apps](platform/app-management/running-apps.md)
    * [App Permissions](platform/app-management/app-permissions.md)
  * [Device Sandbox](platform/standalone-device.md)
  * [Embedding](platform/embedding-apps.md)
  * [Sharing](platform/sharing-apps.md)
  * [Session Inactivity Timeout](platform/session-inactivity-timeout.md)
  * [Query Params Reference](platform/query-params-reference.md)
* [Features](features/README.md)
  * [Devices & OS Versions](features/devices-and-os-versions.md)
  * [Network Traffic Monitor](features/network-traffic-monitor.md)
  * [Debug Logs](features/debug-logs.md)
  * [UI Automation](features/ui-automation.md)
  * [Proxy](features/proxy.md)
  * [Language & Locale](features/language-and-locale.md)
  * [Mock Location](features/mock-location.md)
  * [Deep links](features/deep-links.md)
  * [Launch Params](features/launch-params.md)
  * [Media](features/media.md)
  * [Auto-grant Permissions](features/auto-grant-permissions.md)
  * [Custom Branding](features/custom-branding.md)
  * [Custom Launch Pages](features/custom-launch-pages.md)
  * [Advanced Features](features/advanced-features/README.md)
    * [Android](features/advanced-features/android/README.md)
      * [ADB tunnel](features/advanced-features/android/adb-tunnel.md)
      * [Hide Password Visibility](features/advanced-features/android/hide-password-visibility.md)
    * [Reserved Devices](features/advanced-features/reserved-devices.md)
* [Account](account/README.md)
  * [Invite your team](account/invite-your-team.md)
  * [Single Sign-On](account/single-sign-on.md)
    * [OpenID Connect](account/single-sign-on/openid-connect.md)
    * [SAML](account/single-sign-on/saml.md)
    * [Azure Active Directory](account/single-sign-on/azure-active-directory.md)
    * [Google Workspace (GSuite)](account/single-sign-on/google-workspace-gsuite.md)
  * [Reporting](account/reporting/README.md)
    * [Session History](account/reporting/session-history.md)
    * [Usage Summary](account/reporting/usage-summary.md)
* [Infrastructure](infrastructure/README.md)
  * [Configure Network Access](infrastructure/configure-network-access.md)
  * [Enterprise Hosting Options](infrastructure/enterprise-hosting-options.md)
* [JavaScript SDK](javascript-sdk/README.md)
  * [Configuration](javascript-sdk/configuration.md)
  * [Automation](javascript-sdk/automation/README.md)
    * [Device commands](javascript-sdk/automation/device-commands.md)
    * [Touch interactions](javascript-sdk/automation/touch-interactions.md)
  * [API reference](javascript-sdk/api-reference/README.md)
    * [Initialization](javascript-sdk/api-reference/initialization.md)
    * [Client](javascript-sdk/api-reference/client.md)
    * [Session](javascript-sdk/api-reference/session.md)
    * [Types](javascript-sdk/api-reference/types/README.md)
      * [AdbConnectionInfo](javascript-sdk/api-reference/types/adbconnectioninfo.md)
      * [AppetizeApp](javascript-sdk/api-reference/types/appetizeapp.md)
      * [AndroidElementAttributes](javascript-sdk/api-reference/types/androidelementattributes.md)
      * [Coordinates](javascript-sdk/api-reference/types/coordinates.md)
      * [DeviceInfo](javascript-sdk/api-reference/types/deviceinfo.md)
      * [Element](javascript-sdk/api-reference/types/element.md)
      * [ElementBounds](javascript-sdk/api-reference/types/elementbounds.md)
      * [IOSAccessibilityElement](javascript-sdk/api-reference/types/iosaccessibilityelement.md)
      * [IOSElementAttributes](javascript-sdk/api-reference/types/ioselementattributes.md)
      * [NetworkRequest](javascript-sdk/api-reference/types/networkrequest.md)
      * [NetworkResponse](javascript-sdk/api-reference/types/networkresponse.md)
      * [SessionConfig](javascript-sdk/api-reference/types/sessionconfig.md)
      * [SwipeMove](javascript-sdk/api-reference/types/swipemove.md)
      * [RecordedAction](javascript-sdk/api-reference/types/recordedaction.md)
      * [RecordedSwipeAction](javascript-sdk/api-reference/types/recordedswipeaction.md)
      * [RecordedKeypressAction](javascript-sdk/api-reference/types/recordedkeypressaction.md)
      * [RecordedPosition](javascript-sdk/api-reference/types/recordedposition.md)
      * [RecordedTapAction](javascript-sdk/api-reference/types/recordedtapaction.md)
      * [RecordedTouchAction](javascript-sdk/api-reference/types/recordedtouchaction.md)
      * [UserInteraction](javascript-sdk/api-reference/types/userinteraction.md)
* [Testing](testing/README.md)
  * [Getting Started](testing/getting-started.md)
  * [Writing Tests](testing/writing-tests.md)
  * [Running Tests](testing/running-tests.md)
  * [Test Configuration](testing/test-configuration.md)
  * [Continuous Integration](testing/continuous-integration.md)
  * [Record Tests (experimental)](testing/record-tests-experimental.md)
  * [Trace Viewer](testing/trace-viewer.md)
  * [Web Tests on Mobile Browsers](testing/web-tests-on-mobile-browsers.md)
* [REST API](rest-api/README.md)
  * [Create new app](rest-api/create-new-app.md)
  * [Update existing app](rest-api/update-existing-app.md)
  * [Direct file uploads](rest-api/direct-file-uploads.md)
  * [Delete app](rest-api/delete-app.md)
  * [List apps](rest-api/list-apps.md)
  * [Usage summary](rest-api/usage-summary.md)
  * [Devices & OS Versions](rest-api/devices-and-os-versions/README.md)
    * [v1](rest-api/devices-and-os-versions/v1.md)
  * [IP Blocks](rest-api/ip-blocks/README.md)
    * [v1](rest-api/ip-blocks/v1.md)
* [Guides & Samples](guides-and-samples/README.md)
  * [Impersonation](guides-and-samples/impersonation.md)
  * [Automate Sign-in Flow](guides-and-samples/automate-sign-in-flow.md)
  * [Screenshot Automation](guides-and-samples/screenshot-automation.md)
  * [Unlock Device](guides-and-samples/swipe-a-pattern-to-unlock-an-android-device.md)
  * [Validate Analytics Events](guides-and-samples/open-a-deeplink-and-make-sure-analytics-api-calls-happen.md)
  * [Lock Your Device to One App](guides-and-samples/lock-your-device-to-one-app.md)
  * [Test Accessibility Font Sizes](guides-and-samples/test-accessibility-font-sizes.md)
  * [Common testing scenarios](guides-and-samples/common-testing-scenarios.md)
  * [Samples Repository](https://samples.appetize.io/)
* [Deprecated](deprecated/README.md)
  * [Cross-document messages](deprecated/cross-document-messages.md)
* [Changelog](changelog.md)

## Additional Support

* [Knowledge Base](https://support.appetize.io/)
* [Support Request](https://appetize.io/support-request)
