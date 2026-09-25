# Sessions

A session is one device running one app. `session start` requests the device, waits for it to boot, and leaves a background daemon holding it open until you stop it.

```bash
appetize session start <device-id> <target>
```

| Argument      | What it is                                                                                                                                                          |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `<device-id>` | A device model — `pixel7`, `iphone15pro`. From `appetize device list` or [`GET /v2/service/devices`](https://docs.appetize.io/rest-api/service)                     |
| `<target>`    | A **buildId** — the `id` from `appetize build list`. Previously called publicKey; see [Running apps](https://docs.appetize.io/platform/app-management/running-apps) |

```bash
appetize session start iphone15pro b_a1b2c3 --device-os-version 18.2
appetize session start pixel7 b_a1b2c3 --session-id checkout
appetize session start pixel7 b_a1b2c3 --no-wait
```

Save the session record while you watch it boot — the record goes to stdout, the progress to stderr:

```bash
appetize session start pixel7 b_a1b2c3 > session.json
```

Phases arrive on stderr in this order: `requesting`, `queued`, `starting`, `downloadingApp`, `installingApp`, `launchingApp`, `ready`. Not every session shows all of them — `queued` appears only when you are waiting (for a free device, or for an account concurrency limit to clear) and `downloadingApp` only when the build still has to be fetched. A slow start tells you which of those you are waiting on.

`--no-wait` skips the blocking and returns the session id straight away.

### Watching the session

Every session serves a small viewer page on your machine. `session start` prints its address as `viewerUrl`:

```json
{
  "sessionId": "tidy-pandas-jump",
  "viewerUrl": "http://127.0.0.1:52518/"
}
```

Open it in a browser and you see the device screen, live, while the agent works. The page is only the screen — no logs, no controls, no session details.

It is not read-only. Click and type on the page and the input goes to the device, so you can take over mid-run, fix something by hand, and let the agent carry on. One pointer at a time, and the screen needs focus before typing, so click it first.

{% hint style="warning" %}
No authentication: anyone with access to the machine can open that port and drive the device.
{% endhint %}

A few details worth knowing:

* The port is assigned by the OS each run and cannot be set.
* **One viewer at a time.** Opening the same session in a second tab leaves that tab blank — reload the first one instead.
* Closing the tab does not affect the session, and the viewer closes with `session stop`.
* With `--no-wait`, `session start` returns before the URL is known — read it from the session record instead.

Available since `@appetize/cli` 0.16.0.

## Naming and picking a session

Each session gets a three-word id such as `tidy-pandas-jump`, or the one you pass to `--session-id`. Other commands act on the only running session, so you rarely pass anything:

```bash
appetize screenshot                      # the only session
appetize screenshot --session-id checkout # one of several
```

Starting a session with an id already in use fails.

## Logs

`session start` prints both paths, so you never have to guess where they are.

| Path          | Holds                                      |
| ------------- | ------------------------------------------ |
| `logs.device` | the app's own log lines, streamed as JSONL |
| `logs.daemon` | the CLI's own output                       |

```bash
tail -f ~/.appetize/cli/sessions/checkout/device.log.jsonl
```

## Network traffic

`--proxy` intercepts the app's traffic and captures it to `logs.network`, one JSON event per request, response and error:

```bash
appetize session start pixel7 b_a1b2c3 --proxy --session-id checkout
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
