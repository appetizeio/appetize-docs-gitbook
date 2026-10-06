---
description: The Metro connection for the AI live editing loop.
hidden: true
---

# Metro

Metro carries a save to the device in the [AI live editing](README.md) loop. The agent saves a file, Metro sends it, and the agent looks again.

These steps are for an Expo development build.

## Without Expo

A React Native app that does not use Expo still uses Metro. It does not get an `exp+` URL, and it does not get Expo's tunnel.

The debug build has to be pointed at a Metro server the device can reach. On Android, `adb reverse tcp:8081 tcp:8081` can make `localhost:8081` on the device reach Metro on your computer. iOS has no `adb reverse`, so Metro needs to be on a URL the simulator can open. We have not tried this path.

## 1. Make a development build

This is your app, with the Expo development client in it. It is not Expo Go.

```bash
npx expo install expo-dev-client
```

```json
{
  "build": {
    "development": {
      "developmentClient": true,
      "distribution": "internal",
      "android": { "buildType": "apk" },
      "ios": { "simulator": true }
    }
  }
}
```

Android emulators on Appetize are `x86_64`, so include that ABI:

```bash
npx expo prebuild --platform android
cd android && ./gradlew assembleDebug -PreactNativeArchitectures=x86_64
appetize build upload <apk> --wait
```

`build upload` prints an `id`. That is the build id. Older docs call the same value the public key.

iOS needs a simulator `.app`, zipped. Build it on a Mac, or with EAS from anywhere. Linux cannot build it.

```bash
npx expo run:ios --configuration Debug
zip -r MyApp.zip MyApp.app
appetize build upload <zip> --wait
```

## 2. Start Metro

```bash
npx expo start --dev-client --tunnel
```

If Expo asks for `@expo/ngrok`, install it and run the command again. Leave Metro running. Copy the `exp+` URL it prints. That URL is `<metro-url>` below.

## 3. Open that URL on the device

```bash
appetize session start <device> <build-id>
appetize open '<metro-url>'
```

`<device>` comes from `appetize device list`, for example `pixel7` or `iphone15pro`.

`<build-id>` is the `id` from `appetize build upload`, or from `appetize build list`. This is the value older docs call the public key.

`<metro-url>` is the whole `exp+` line from Metro. Keep the quotes so the shell does not split it.

The first launch can show a developer menu. Tap **Continue** if you see it.

<figure><img src="../../.gitbook/assets/metro-developer-menu.png" alt="A developer menu with a Continue button over the app."><figcaption><p>Tap Continue, then close the menu.</p></figcaption></figure>

`session start` prints a `viewerUrl`. Open it in a window next to your editor to watch the device while you work.

## 4. Save, then look

Change some JavaScript or a style, and save. The device updates. The app stays open, so the agent checks the same screen instead of starting over.

```bash
appetize inspect --select-text '<something on the screen>'
appetize screenshot after-edit
```

![The editor is on the left and the viewer is on the right. The save swaps the plain die for an animated one. The die spins on each roll, and the score keeps counting.](../../.gitbook/assets/metro-fast-refresh.mp4)

<figure><img src="../../.gitbook/assets/metro-live-change.png" alt="Before, a plain die shows a question mark. After a save, the die is tilted mid-spin and the rounds count is 1."><figcaption><p>One save swapped in the animated die. The game kept its score.</p></figcaption></figure>

Stop the session when you are done:

```bash
appetize session stop
```

## If nothing changes

| What you see | What to try |
| --- | --- |
| Metro offers Expo Go | Stay on the development build. |
| The device shows the Development Build launcher | Run `appetize open '<metro-url>'` again. The first open can arrive while the app is still starting. |
| The device looks for `10.0.2.2:8081` | Open `<metro-url>`. That address is the emulator, not your computer. |
| A blank screen | Wait until Metro says `Bundled`. The developer menu may be in the way. |
| The app opens, then closes | The Android build needs `x86_64`. The iOS build needs to be a simulator `.app`, not an `.ipa`. |
| A save does nothing | Check that Metro is still running and that it printed a new bundle. |
