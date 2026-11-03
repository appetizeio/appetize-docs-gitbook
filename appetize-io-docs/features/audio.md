---
description: >-
  Stream the device's audio output to your browser. This lets you hear in-app
  sounds, media playback, and the TalkBack screen reader during a session.
---

# Audio

{% hint style="info" %}
Audio is currently supported on **Android** devices only.
{% endhint %}

### Enabling audio

#### On the App Page

Add the [`audio`](../javascript-sdk/configuration.md#audio) query parameter to your app or embed URL:

```
https://appetize.io/app/<buildId|publicKey>?device=pixel7&audio=true
```

#### With the JavaScript SDK

Set `audio: true` in your session config:

```typescript
const client = await window.appetize.getClient("#appetize")

const session = await client.startSession({
    device: "pixel7",
    audio: true,
})
```

### Capturing audio frames

When audio is enabled, the session emits an `audio` event as frames arrive. The event includes the frame `buffer`, its `codec`, and the frame `duration`. Use it to record or mux audio alongside the `video` event:

```typescript
session.on("audio", ({ buffer, codec, duration }) => {
    // `buffer` contains the AAC audio frame
    // `codec` is "aac"
    // `duration` is the frame duration in seconds
})
```

### Live sample

Hear audio output combined with the TalkBack screen reader:

{% embed url="https://samples.appetize.io/audio_talkback_experience/launch.html" %}
