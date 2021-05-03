# Uploading apps

You may upload apps directly via your web browser at [https://appetize.io/upload](https://appetize.io/upload), or you may upload programmatically via our [API](../api/create-new-app.md). 

We also have many 3rd party integrations with tools such as [fastlane](https://docs.fastlane.tools/actions/appetize/), [Bitrise](https://www.bitrise.io/integrations/steps/appetize-deploy), and [Expo](https://expo.io/). 

{% tabs %}
{% tab title="iOS" %}
For iOS, upload a `.zip` or `.tar.gz` file containing your compressed `.app` bundle.

Your `.app` bundle must represent a iOS Simulator build of your app. A simulator build can be run in the iOS Simulator via Xcode. This is different than a IPA file, which is compiled for ARM architecture CPUs and can only be run on physical iOS devices. 

One way to get the iOS Simulator build is to run your app in an iOS Simulator, and then to find the file that is automatically generated. After running in the iOS Simulator via Xcode, look in:

`~/Library/Developer/Xcode/DerivedData/<project-name>/Build/Products/Debug-iphonesimulator/`

You may also generate the iOS Simulator build of your app by building it directly via the command line using xcodebuild. 

If you have a .xcodeproj file, you may run: 

`xcodebuild -sdk iphonesimulator`

If you have a .xcworkspace file, you may run: 

`xcodebuild -sdk iphonesimulator -workspace <your_workspace_name>.xcworkspace/ -scheme <your-scheme> -configuration Debug`.

In order to get the name of your Scheme, you may run: 

`xcodebuild -list -workspace <your_workspace_name>.xcworkspace`

Once the build command completes successfully, you may then zip the `.app` bundle found in: 

`build/Debug-iphonesimulator/`

If you are having trouble running your uploaded iOS app in Appetize.io, please find our troubleshooting steps at [https://support.appetize.io/help/error-installing-or-running-app-on-ios](https://support.appetize.io/help/error-installing-or-running-app-on-ios).

If you are using Xamarin to develop your apps, please see our specific instructions at [https://support.appetize.io/help/how-to-upload-xamarin-apps-to-appetize-io](https://support.appetize.io/help/how-to-upload-xamarin-apps-to-appetize-io).

### **Note about Xcode 12 and iOS 14**

When building via the command line with Xcode 12, some users are encountering an issue with Apple's new arm64 architecture support in simulator builds. You may find the following troubleshooting steps useful:

[https://stackoverflow.com/questions/64036180/error-module-was-created-for-incompatible-target-arm64-apple-ios8-0/64048460\#64048460](https://stackoverflow.com/questions/64036180/error-module-was-created-for-incompatible-target-arm64-apple-ios8-0/64048460#64048460)
{% endtab %}

{% tab title="Android" %}
For Android, upload the `.apk` containing your app. 

After your app is built, either via Android Studio or by running the command `./gradlew assembleDebug` in your project directory, look in:

`<project-name>/<app-module-name>/build/outputs/apk/`

If you are having trouble running your uploaded Android app in Appetize.io, we recommend trying to run the same APK on a physical Android device or Android emulator locally over ADB. 

Once your device or emulator is connected via ADB, you can install it using a command like:

`adb install -r example.apk`
{% endtab %}
{% endtabs %}





