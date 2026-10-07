---
description: Use Metro and Fast Refresh so a save updates the running app.
hidden: true
---

# React Native

Use Metro and Fast Refresh so a save updates the running app and keeps its state.

The agent runs on the left. The CLI's viewer is on the right.

{% embed url="https://cdn.jsdelivr.net/gh/appetizeio/appetize-docs-gitbook@31d9ddde859d8f6c6b729e485190673ba535ea29/.gitbook/assets/development-loop.mp4" %}

## 1. Upload a development build

```bash
npx expo install expo-dev-client
```

Android:

```bash
npx expo prebuild --platform android
cd android && ./gradlew assembleDebug -PreactNativeArchitectures=x86_64
appetize build upload <apk> --wait
```

iOS, on a Mac:

```bash
npx expo run:ios
zip -r MyApp.zip MyApp.app
appetize build upload <zip> --wait
```

The upload prints an `id`. That is `<build-id>`. Older docs call it the public key.

## 2. Start Metro

```bash
npx expo start --dev-client --tunnel
```

Copy the `exp+` URL it prints. That is `<metro-url>`.

## 3. Open the app

```bash
appetize session start <device> <build-id>
appetize open '<metro-url>'
```

`<device>` comes from `appetize device list`, such as `pixel7` or `iphone15pro`.

If the Development Build launcher shows, run `open` again. Tap **Continue** if a developer menu appears.

Open the `viewerUrl` from `session start` beside your editor.

## 4. Save, then look

Save a file. The screen updates and the app stays open.

```bash
appetize session stop
```

## Without Expo

Start Metro with `npx react-native start`. On Android, `adb reverse tcp:8081 tcp:8081` points the device at it. On iOS, Metro needs a URL the simulator can reach.
