---
description: >-
  Connect an Expo development build on Appetize to a local Metro server through
  Expo's tunnel, then apply JavaScript changes without rebuilding.
---

# Metro

Metro is one way to [live edit](README.md) an app on Appetize. Expo's tunnel makes the Metro server on your machine reachable from the cloud device. The CLI opens that URL in your development build.

```text
editor -> Metro -> Expo tunnel -> development build on Appetize
CLI -----------------------> session, taps, and screenshots
```

## Before you start

* Node 22 or later, and `@appetize/cli`
* `APPETIZE_API_TOKEN`, from [API tokens](../../account/api-tokens.md)
* An Expo project with [`expo-dev-client`](https://docs.expo.dev/develop/development-builds/introduction/)
* Android SDK on Linux, Windows, or macOS for an Android build
* Xcode on macOS, or an EAS simulator build, for iOS

```bash
npx expo install expo-dev-client
```

The development profile builds an installable debug app and leaves JavaScript to Metro:

```json
{
  "build": {
    "development": {
      "developmentClient": true,
      "distribution": "internal",
      "android": {
        "buildType": "apk"
      },
      "ios": {
        "simulator": true
      }
    }
  }
}
```

## Build and upload

A debug build is required. A release build has no development client and cannot load Metro.

### Android

Appetize Android emulators run `x86_64`. Include that ABI. Limiting the build to it also keeps a React Native debug APK smaller:

```bash
npx expo prebuild --platform android
cd android
./gradlew assembleDebug -PreactNativeArchitectures=x86_64
```

Upload the APK and keep the build id it prints:

```bash
appetize build upload ./android/app/build/outputs/apk/debug/app-debug.apk --wait
```

See [Uploading Android apps](../../platform/app-management/uploading-apps/android.md).

### iOS

Appetize accepts an iOS Simulator `.app`, compressed as `.zip` or `.tar.gz`. Produce it with Xcode on macOS, or with EAS from any operating system. A Linux machine cannot compile it locally.

```bash
npx expo run:ios --configuration Debug
```

The built app is under the Xcode products directory, in `Debug-iphonesimulator`. Compress that `.app` and upload it:

```bash
zip -r MyApp.zip MyApp.app
appetize build upload ./MyApp.zip --wait
```

For EAS, set `ios.simulator` to `true` on the development profile, then run:

```bash
npx eas-cli@latest build --platform ios --profile development
```

See [Uploading iOS apps](../../platform/app-management/uploading-apps/ios.md).

## Start Metro

From the project, expose Metro through Expo's tunnel:

```bash
npx expo start --dev-client --tunnel
```

If Expo reports that `@expo/ngrok` is missing, install it with `npx expo install @expo/ngrok` and run the command again.

Leave this process running. Its development-client URL looks like this:

```text
exp+my-app://expo-development-client/?url=https%3A%2F%2Fxxxx.exp.direct
```

`my-app` is the Expo slug. Copy the whole `exp+` URL. It is already encoded.

## Open it on the device

```bash
appetize session start pixel7 b_a1b2c3
appetize open 'exp+my-app://expo-development-client/?url=https%3A%2F%2Fxxxx.exp.direct'
```

Use `iphone15pro`, or another id from `appetize device list`, for an iOS simulator build. Quote the URL so the shell does not split it.

Metro prints `Bundled` when the device has loaded the app. The development client can show its menu on the first launch. When **Continue** is visible, dismiss it:

```bash
appetize tap --select-text Continue
```

<figure><img src="../../.gitbook/assets/metro-developer-menu.png" alt="The Expo development client menu covering the app, with a Continue button."><figcaption><p>The development client menu on first launch. Dismiss it before driving the app.</p></figcaption></figure>

Confirm the app itself is on screen:

```bash
appetize inspect --select-text 'Your screen title' --timeout 30000
appetize screenshot app-loaded
```

`session start` also prints a local `viewerUrl`. Open that page to watch the device while you edit.

## Edit

Save a JavaScript or `StyleSheet` change. Metro sends it through the same tunnel, and Fast Refresh applies it in the running app. The native process stays up, so screen state that Fast Refresh can preserve stays in place.

<figure><img src="../../.gitbook/assets/metro-after-refresh.png" alt="The same roll remains on screen after the subtitle has changed."><figcaption><p>After a save, the subtitle has changed and the roll is still there.</p></figcaption></figure>

![Fast Refresh updates the subtitle while the roll stays on screen.](../../.gitbook/assets/metro-fast-refresh.mp4)

```bash
appetize screenshot after-edit
appetize session stop
```

Stop the session when you are finished. It holds the device until you do.

## Replace the Android build

A running Android session prints `adbSerial`. You can install a new native build without starting over, then open the current Metro URL again:

```bash
adb connect 127.0.0.1:57275
adb -s 127.0.0.1:57275 install -r ./android/app/build/outputs/apk/debug/app-debug.apk
appetize open 'exp+my-app://expo-development-client/?url=https%3A%2F%2Fxxxx.exp.direct'
```

Use the serial from your own `session start` output. iOS has no equivalent install command. Upload the new simulator build and start a session against its build id.

## Troubleshooting

| What you see | What to do |
| --- | --- |
| Metro offers Expo Go | Stay on the development build. The running app is your uploaded build, not Expo Go. |
| The device tries `10.0.2.2:8081` and never bundles | The development client fell back to the emulator's own loopback address. Open the `exp+` tunnel URL printed by Metro. |
| A blank white screen | Wait for Metro to print `Bundled`. Then inspect again. The development menu may be covering the app. |
| The bundle loads, then the app closes | Confirm the APK contains `x86_64` and that the iOS upload is a simulator build, not an `.ipa`. |
| JavaScript changes do not appear | Confirm the Metro process is still running and that its log shows a new bundle after the save. |
| `APPETIZE_API_TOKEN must be set` | Export a token before uploading or starting a session. See [Getting started](../../ai-agents/getting-started.md). |
