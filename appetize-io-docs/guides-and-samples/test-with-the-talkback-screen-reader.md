---
description: >-
  TalkBack is Android's built-in screen reader. Enabling it on an Appetize
  device lets you verify that your app is accessible.
---

# Test with the TalkBack Screen Reader

[TalkBack](https://support.google.com/accessibility/android/answer/6283677) is preinstalled on Appetize Android devices but disabled by default. You enable it for a session by running a few `adb` commands and turning on audio so you can hear it.

{% hint style="warning" %}
TalkBack registers itself as an accessibility service. Appetize's automation helper (`io.appetize.automations`) is also an accessibility service, so it must be uninstalled before TalkBack can take over. **This disables the automation engine** (`findElement`, `playAction`, recorded actions) for the rest of the session. Start a fresh session to get automation back.
{% endhint %}

### Prerequisites

* An **Android** device. TalkBack and `adb` commands are Android-only.
* [Audio enabled](../features/audio.md) on the session, so you can hear TalkBack speak.

### Enable TalkBack

Run the following adb shell commands on the device, in order:

```bash
# Remove the Appetize automation helper (it conflicts with TalkBack)
adb shell pm uninstall io.appetize.automations

# Grant TalkBack the runtime permissions it needs
adb shell pm grant com.google.android.marvin.talkback android.permission.POST_NOTIFICATIONS
adb shell pm grant com.google.android.marvin.talkback android.permission.READ_PHONE_STATE

# Set TalkBack as the active accessibility service
adb shell settings put secure enabled_accessibility_services \
  com.google.android.marvin.talkback/com.google.android.marvin.talkback.TalkBackService
```

### Running the commands on Appetize

You can run these in three ways, depending on your workflow.

#### With the JavaScript SDK

Use [`session.adbShellCommand()`](../javascript-sdk/api-reference/session.md#adbshellcommand). It runs the part **after** `adb shell`. Enable audio in the session config so TalkBack is audible:

```typescript
const client = await window.appetize.getClient("#appetize")

const session = await client.startSession({
    device: "pixel7",
    audio: true,
})

await session.adbShellCommand("pm uninstall io.appetize.automations")
await session.adbShellCommand("pm grant com.google.android.marvin.talkback android.permission.POST_NOTIFICATIONS")
await session.adbShellCommand("pm grant com.google.android.marvin.talkback android.permission.READ_PHONE_STATE")
await session.adbShellCommand(
    "settings put secure enabled_accessibility_services com.google.android.marvin.talkback/com.google.android.marvin.talkback.TalkBackService"
)
```

#### At session start

Use `adbShellCommand` when you want TalkBack enabled as soon as the session starts. Since `adbShellCommand` accepts one shell string, chain the commands together:

{% tabs %}
{% tab title="App or embed URL" %}
```url
https://appetize.io/app/<buildId|publicKey>?device=pixel7&audio=true&adbShellCommand=pm%20uninstall%20io.appetize.automations%20%26%26%20pm%20grant%20com.google.android.marvin.talkback%20android.permission.POST_NOTIFICATIONS%20%26%26%20pm%20grant%20com.google.android.marvin.talkback%20android.permission.READ_PHONE_STATE%20%26%26%20settings%20put%20secure%20enabled_accessibility_services%20com.google.android.marvin.talkback%2Fcom.google.android.marvin.talkback.TalkBackService
```
{% endtab %}

{% tab title="JavaScript SDK" %}
```typescript
const client = await window.appetize.getClient("#appetize")

const session = await client.startSession({
    device: "pixel7",
    audio: true,
    adbShellCommand: "pm uninstall io.appetize.automations && pm grant com.google.android.marvin.talkback android.permission.POST_NOTIFICATIONS && pm grant com.google.android.marvin.talkback android.permission.READ_PHONE_STATE && settings put secure enabled_accessibility_services com.google.android.marvin.talkback/com.google.android.marvin.talkback.TalkBackService",
})
```
{% endtab %}
{% endtabs %}

#### With an ADB tunnel

Use an [ADB tunnel](../features/advanced-features/android/adb-tunnel.md) when you want to run standard `adb shell` commands from your machine or from Android Studio.

1. Start the session with `audio=true&enableAdb=true`.
2. Connect to the device with the generated ADB command.
3. Run the commands from the **Enable TalkBack** section with `adb shell ...`.

This is useful when you already debug sessions through ADB and want the same workflow here.

### Live sample

Hear audio output combined with the TalkBack screen reader:

{% embed url="https://samples.appetize.io/audio_talkback_experience/launch.html" %}
