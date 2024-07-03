---
description: To get started, Appetize requires the APK containing your application.
---

# Android

## Finding your APK file

### With Android Studio

Select **Build** -> **Build APK(s)** -> **Build APK(s)** or **Build** -> **Generated Signed APK** (and following the prompts)

<figure><img src="../../.gitbook/assets/image (3) (1) (1).png" alt="" width="563"><figcaption><p>Building with Android Studio</p></figcaption></figure>

Once the build is complete you can locate the `.apk` file by selecting `locate` in the dialog that appears

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-02 at 15.07.06.png" alt="" width="368"><figcaption><p>Select <code>locate</code> in the dialog to navigate to the apk</p></figcaption></figure>

or by navigating to

```
{project name}/{app module name}/build/outputs/apk/
```

### With Gradle

Generate your build with `gradle` by running the `assemble` command for your preferred app build variant e.g. `debug` variant

```
./gradlew assembleDebug
```

Once the build is complete you can locate the `.apk` file by navigating to

```
{project name}/{app module name}/build/outputs/apk/
```

## Converting AAB to APK

Appetize currently only support `apk` files for Android. In order to get your application to work with Appetize you will need to convert your `aab` to an `apk` by making use of the [`bundletool`](https://developer.android.com/tools/bundletool) provided by Google.

#### Generate Universal APKS

```shell-session
bundletool build-apks --bundle=/<your app>/{aab name}.aab \
    --output=/{your app}/{app name}.apks \
    --mode=universal
```

#### Generate Single APK file from the Universal APKs

```
unzip -p /{your app}/{app name}.apks universal.apk > /{your app}/{app name}.apk
```

## Troubleshooting

If you are having trouble running your uploaded Android app in Appetize, we recommend trying to run the same APK on the standard Google-provided Android emulator locally over ADB.

Once your emulator is launched and available via `adb devices`, you can install it using the `install` command:

```
adb install -r {your app}.apk
```

or by simply dragging over the `apk` into the emulator window.

Also check our [Knowledge Base](https://support.appetize.io/) for frequently asked questions and solutions.
