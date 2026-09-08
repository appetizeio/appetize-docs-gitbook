# Sessions

A session is one device running one app. `session start` requests the device, waits for it to boot, and leaves a background daemon holding it open until you stop it.

```bash
appetize session start <device-id> <target>
```

| Argument      | What it is                                                                                                                                      |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| `<device-id>` | A device model — `pixel7`, `iphone15pro`. From `appetize device list` or [`GET /v2/service/devices`](https://docs.appetize.io/rest-api/service) |
| `<target>`    | A build id from `appetize build list`, or an app's public key                                                                                   |

```bash
appetize session start iphone15pro b_zt5w2yb3hn6vqk4a --device-os-version 18.2
appetize session start pixel7 b_zt5w2yb3hn6vqk4a --session-id checkout
appetize session start pixel7 b_zt5w2yb3hn6vqk4a --no-wait
```

Phases are logged to stderr while the device boots: `requesting`, `queued`, `starting`, `downloadingApp`, `installingApp`, `launchingApp`, `ready`. A slow start tells you whether you are queued for capacity or waiting on an install. `--no-wait` skips the blocking and returns the session id straight away.

## Naming and picking a session

Each session gets a three-word id such as `tidy-pandas-jump`, or the one you pass to `--session-id`. Other commands act on the only running session, so you rarely pass anything:

```bash
appetize screenshot                      # the only session
appetize screenshot --session-id checkout # one of several
```

Starting a session with an id already in use fails.

## Logs

`session start` prints both paths, so you never have to guess where they are.

| Path          | Holds                                                        |
| ------------- | ------------------------------------------------------------ |
| `logs.device` | the app's own log lines, streamed as JSONL                   |
| `logs.daemon` | the CLI's own output — read this when the session misbehaves |

```bash
tail -f ~/.appetize/cli/sessions/checkout/device.log.jsonl
```

## Network traffic

`--proxy` intercepts the app's traffic and captures it to `logs.network`, one JSON event per request, response and error:

```bash
appetize session start pixel7 b_zt5w2yb3hn6vqk4a --proxy --session-id checkout
```

```bash
jq -r 'select(.type == "response") | "\(.response.status) \(.request.method) \(.request.url)"' \
  ~/.appetize/cli/sessions/checkout/network.jsonl
```

Pass a url instead — `--proxy http://proxy:8080` — to route through a proxy of your own. That routes traffic without intercepting it, so nothing is captured.

{% hint style="info" %}
Interception rewrites TLS, so an app that pins certificates may not work under it. Retry without `--proxy` if calls fail only when it is on.
{% endhint %}

## adb

An Android session prints an `adbSerial`. Connect to it and the device behaves like any local emulator:

```bash
adb connect 127.0.0.1:57275   # the adbSerial from session start
adb logcat
adb install ./build-under-test.apk
adb shell dumpsys activity
```

The connection lasts as long as the session, and `adb devices` lists it while it does. iOS sessions have no `adbSerial`.

## Stopping

```bash
appetize session stop
```

The device is released and the daemon shuts down. It reports the id even if the daemon had already exited, so calling it twice is safe. A session holds a device for as long as it runs, so stop it when you are done.
