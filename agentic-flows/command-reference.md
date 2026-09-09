# Command reference

Every command, the values it accepts and what it prints. `appetize <command> --help` prints the same flags and examples at the terminal.

| Command                                                   | What it does                                     |
| --------------------------------------------------------- | ------------------------------------------------ |
| [`session start`](command-reference.md#session-start)     | Start a device session and wait until it's ready |
| [`session stop`](command-reference.md#session-stop)       | Release the device and stop the daemon           |
| [`build list`](command-reference.md#build-list)           | List uploaded builds and their session targets   |
| [`build upload`](command-reference.md#build-upload)       | Upload a build as a session target               |
| [`device list`](command-reference.md#device-list)         | List device models and their OS versions         |
| [`inspect`](command-reference.md#inspect)                 | Capture the view hierarchy                       |
| [`tap`](command-reference.md#tap)                         | Tap an element or a screen position              |
| [`swipe`](command-reference.md#swipe)                     | Scroll in a direction, or drag along a path      |
| [`type`](command-reference.md#type)                       | Type text and named keys                         |
| [`press`](command-reference.md#press)                     | Press a hardware button                          |
| [`rotate`](command-reference.md#rotate)                   | Rotate the device                                |
| [`screenshot`](command-reference.md#screenshot)           | Write a PNG of the screen                        |
| [`recording start`](command-reference.md#recording-start) | Start capturing device video to an MP4           |
| [`recording stop`](command-reference.md#recording-stop)   | Close the video stream and the file              |
| [`skill install`](command-reference.md#skill-install)     | Install the agent skill for coding agents        |

Global flags: `--version` prints the CLI version, `--help` prints usage for the CLI or any command.

`--session-id` is accepted by every command that acts on a device. On `session start` it names the session being created; elsewhere it picks which running session to act on, defaulting to the only one.

Every command follows the same split: **stdout carries the result, stderr carries diagnostics** — progress, warnings and errors alike. That is what makes the commands scriptable — `appetize session start … > session.json` leaves valid JSON in the file with the boot progress still on screen, where merging the streams with `2>&1` would corrupt it. Commands exit `0` on success and non-zero on failure — including when a `--timeout` expires, which is what makes it usable as a wait.

## session start

Requests a device, waits for the app to launch, and leaves a daemon holding the session open.

```bash
appetize session start <device-id> <target> [options]
```

| Argument      | Values                                                                                                                                                         |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `<device-id>` | Any `id` from `appetize device list` or [`GET /v2/service/devices`](https://docs.appetize.io/rest-api/service), e.g. `pixel7`, `iphone15pro`                   |
| `<target>`    | A **buildId** — the `id` from `appetize build list`, previously called publicKey ([what it is](https://docs.appetize.io/platform/app-management/running-apps)) |

| Flag                  | Values                                      | Meaning                                                 |
| --------------------- | ------------------------------------------- | ------------------------------------------------------- |
| `--device-os-version` | Any `osVersions` entry for that device      | OS version to boot, e.g. `18.2` (iOS) or `14` (Android) |
| `--endpoint`          | An Appetize URL                             | Overrides `APPETIZE_ENDPOINT`                           |
| `--no-wait`           | —                                           | Return without waiting for the device to be ready       |
| `--proxy`             | `intercept` (default when bare), `http://…` | Capture traffic, or route through your own proxy        |
| `--session-id`        | Letters, digits, `.`, `-`, `_`              | Name the session; defaults to a generated three-word id |

**Examples**

```bash
appetize session start iphone15pro b_a1b2c3
appetize session start pixel7 b_a1b2c3 --device-os-version 14
appetize session start pixel7 b_a1b2c3 --session-id checkout --proxy
```

Prints `{ adbSerial, baseUrl, controlSocket, logs, sessionId }` once the device is ready, or `{ logs, sessionId }` immediately with `--no-wait`. `adbSerial` is Android only. `logs` gains a `network` path when traffic is intercepted with `--proxy`.

Phases are logged to stderr as the session starts, in this order: `requesting`, `queued`, `starting`, `downloadingApp`, `installingApp`, `launchingApp`, `ready`. `queued` and `downloadingApp` are skipped when they do not apply. The result itself goes to stdout, so `> session.json` captures the JSON and leaves the progress on screen. Starting a session with an id already in use fails.

## session stop

Releases the device and shuts the daemon down.

```bash
appetize session stop [--session-id <id>]
```

**Examples**

```bash
appetize session stop
appetize session stop --session-id checkout
```

Prints `{ ended: true, sessionId }`. It reports the id even if the daemon had already exited, so it is safe to call twice.

## build list

Lists one page of the account's uploaded builds, newest first.

```bash
appetize build list [options]
```

| Flag         | Values                   | Meaning                       |
| ------------ | ------------------------ | ----------------------------- |
| `--app`      | A bundle or package id   | Filter to one app             |
| `--endpoint` | An Appetize URL          | Overrides `APPETIZE_ENDPOINT` |
| `--limit`    | `1`–`200` (default `10`) | Builds per page               |
| `--page`     | `1` and up (default `1`) | Page of results to fetch      |

**Examples**

```bash
appetize build list
appetize build list --app com.example.app
appetize build list --app com.example.app --page 2
```

Prints `{ builds, nextPage, total }`. Each build carries `id` — the buildId, which is what `session start` takes as its target — plus `appId`, `platform`, `versionName`, `buildNumber` and `created`. Pass a non-null `nextPage` back as `--page` to continue. Requires `APPETIZE_API_TOKEN`.

Same data as [`GET /v2/builds`](https://docs.appetize.io/rest-api/builds) in the REST API; `--app` filters the way [`GET /v2/apps/{platform}/{appId}/builds`](https://docs.appetize.io/rest-api/app-builds) does.

## build upload

Uploads a build and returns a target you can start a session against immediately.

```bash
appetize build upload <file> [options]
```

| Argument | Values                                                     |
| -------- | ---------------------------------------------------------- |
| `<file>` | `.apk`, `.apks` (Android); `.zip`, `.tar.gz`, `.tgz` (iOS) |

| Flag         | Values                          | Meaning                                         |
| ------------ | ------------------------------- | ----------------------------------------------- |
| `--endpoint` | An Appetize URL                 | Overrides `APPETIZE_ENDPOINT`                   |
| `--note`     | Any string                      | Note stored with the build                      |
| `--tags`     | Comma separated strings         | Tags stored with the build                      |
| `--timeout`  | Milliseconds (default `120000`) | How long `--wait` waits                         |
| `--wait`     | —                               | Wait for app id and version metadata to resolve |

**Examples**

```bash
appetize build upload ./app.apk
appetize build upload ./app.zip
appetize build upload ./app.apk --wait
appetize build upload ./app.apk --tags beta,latest --note "PR 42"
```

Prints `{ created, id, platform }`. The extension decides the platform, and any other file is refused before uploading.

Appetize fills in `appId`, `versionName` and `buildNumber` by processing the file after the upload responds. That takes a few seconds and is not needed to start a session; `--wait` polls until they appear and prints the full `build list` shape. Requires `APPETIZE_API_TOKEN`.

Wraps [`POST /v2/builds`](https://docs.appetize.io/rest-api/builds) in the REST API, and `--wait` polls [`GET /v2/builds/{buildId}`](https://docs.appetize.io/rest-api/builds) until the metadata lands.

## device list

Lists the device models available to you.

```bash
appetize device list [options]
```

| Flag         | Values           | Meaning                       |
| ------------ | ---------------- | ----------------------------- |
| `--endpoint` | An Appetize URL  | Overrides `APPETIZE_ENDPOINT` |
| `--platform` | `ios`, `android` | Filter by platform            |

**Examples**

```bash
appetize device list
appetize device list --platform ios
```

Prints `{ devices }`. Each device carries `id` — the `<device-id>` `session start` takes — plus `name`, `platform` and `osVersions`, the values `--device-os-version` accepts. Needs no API token.

Same list as [`GET /v2/service/devices`](https://docs.appetize.io/rest-api/service) in the REST API, which is also public — reach for it when you want the device ids from something other than a terminal.

## inspect

Writes the view hierarchy of the screen, or of one element, to a file.

```bash
appetize inspect [output] [options]
```

| Argument   | Values                                                    |
| ---------- | --------------------------------------------------------- |
| `[output]` | A path; defaults to `inspect.json`, `.json` added for you |

| Flag               | Values                          | Meaning                        |
| ------------------ | ------------------------------- | ------------------------------ |
| `--select-text`    | Exact string, or `/regex/flags` | Scope to a matching element    |
| `--select-test-id` | Exact string                    | Scope by test id               |
| `--select-index`   | `0` and up                      | Which match when several       |
| `--timeout`        | Milliseconds                    | Wait this long for the element |
| `--pretty`         | — (default `false`)             | Indent the JSON                |

**Examples**

```bash
appetize inspect
appetize inspect --select-text 'Log in'
appetize inspect hierarchy.json --pretty
appetize inspect --select-test-id home-feed --timeout 5000
```

Writes `{ platform, root }` — each node carrying `attributes`, `bounds` and `children` — and prints `{ bytes, nodes, output }`. Only currently visible elements appear.

## tap

Taps an element, or a point on the screen.

```bash
appetize tap [options]
```

| Flag                | Values                          | Meaning                                     |
| ------------------- | ------------------------------- | ------------------------------------------- |
| `--select-text`     | Exact string, or `/regex/flags` | Match by text                               |
| `--select-test-id`  | Exact string                    | Match by test id                            |
| `--select-index`    | `0` and up                      | Which match when several                    |
| `--select-position` | `x,y` with each `0`–`1`         | A screen position instead of an element     |
| `--select-x`        | `0`–`1`, outside allowed        | Horizontal point within the matched element |
| `--select-y`        | `0`–`1`, outside allowed        | Vertical point within the matched element   |
| `--timeout`         | Milliseconds                    | Wait this long for the element              |

**Examples**

```bash
appetize tap --select-text 'Log in'
appetize tap --select-test-id save
appetize tap --select-text '/^Item \d+/i' --select-index 2
appetize tap --select-position 0.5,0.75
appetize tap --select-test-id slider --select-x 0.9
appetize tap --select-test-id dialog --select-x=-0.1
```

Prints `{ tapped: true }`. Pick one of `--select-text`, `--select-test-id` or `--select-position`. Combining an element selector with `--select-x` / `--select-y` taps a point within that element, and values outside `0`–`1` reach just beyond its edge — write those as `--select-x=-0.1` so the leading `-` isn't read as a flag.

## swipe

Scrolls the screen, or drags from one point to another.

```bash
appetize swipe [options]
```

| Flag                                       | Values                          | Meaning                                     |
| ------------------------------------------ | ------------------------------- | ------------------------------------------- |
| `--direction`                              | `up`, `down`, `left`, `right`   | Scroll the screen this way                  |
| `--distance`                               | `0`–`1`                         | Travel as a fraction of the screen          |
| `--from-text`, `--to-text`                 | Exact string, or `/regex/flags` | End point by text                           |
| `--from-test-id`, `--to-test-id`           | Exact string                    | End point by test id                        |
| `--from-index`, `--to-index`               | `0` and up                      | Which match when several                    |
| `--from-position`, `--to-position`         | `x,y` with each `0`–`1`         | End point as a screen position              |
| `--from-x`, `--from-y`, `--to-x`, `--to-y` | `0`–`1`, outside allowed        | Point within the matched element            |
| `--duration`                               | Milliseconds                    | How long the gesture travels                |
| `--timeout`                                | Milliseconds                    | Wait this long for `--from`/`--to` elements |

**Examples**

```bash
appetize swipe --direction up
appetize swipe --direction up --distance 0.25
appetize swipe --direction left --from-test-id card --from-index 1
appetize swipe --from-position 0.5,0.75 --to-position 0.5,0.3
appetize swipe --from-text 'Drag me' --from-y 0.9 --to-test-id drop-zone
```

Prints `{ swiped: true }`. Two shapes are valid: a `--direction` with an optional `--from-*` starting point, or a `--from-*` and a `--to-*` point forming a path. Mixing `--direction` with `--to-*` is an error, as is `--distance` without `--direction`.

## type

Types text into the focused field.

```bash
appetize type <text> [options]
```

| Argument | Values                                                    |
| -------- | --------------------------------------------------------- |
| `<text>` | Any string; `{...}` names a key, `{{` types a literal `{` |

| Flag      | Values       | Meaning            |
| --------- | ------------ | ------------------ |
| `--delay` | Milliseconds | Wait between steps |

Named keys: `Enter`, `Tab`, `Backspace`, `ArrowUp`, `ArrowDown`, `ArrowLeft`, `ArrowRight`. Add a repeat count as `{Backspace>16/}`.

**Examples**

```bash
appetize type 'hello{Enter}'
appetize type '{Backspace>16/}'
appetize type 'user@example.com{Tab}hunter2{Enter}' --delay 50
```

Prints `{ typed: true }`. An unclosed token or an unsupported key name fails without typing anything. Typing does not focus a field — tap it first.

## press

Presses a hardware button.

```bash
appetize press <button>
```

| Argument   | Values                                                                                        |
| ---------- | --------------------------------------------------------------------------------------------- |
| `<button>` | `home`, `lock` (both platforms); `back`, `menu`, `unlock`, `volumeUp`, `volumeDown` (Android) |

**Examples**

```bash
appetize press home
appetize press volumeUp
appetize press back
```

Prints `{ pressed: true }`. An unknown name is refused with the full list of buttons. The CLI does not check the button against the session's platform, so an Android-only button on an iOS session is not rejected by the CLI.

## rotate

Rotates the device.

```bash
appetize rotate <orientation>
```

| Argument        | Values                                                      |
| --------------- | ----------------------------------------------------------- |
| `<orientation>` | `portrait`, `landscapeLeft`, `landscapeRight`, `upsideDown` |

**Examples**

```bash
appetize rotate portrait
appetize rotate landscapeLeft
```

Prints the resulting orientation.

## screenshot

Writes a PNG of the current screen.

```bash
appetize screenshot [output]
```

| Argument   | Values                                                               |
| ---------- | -------------------------------------------------------------------- |
| `[output]` | A path; defaults to `screenshot`, a matching extension added for you |

**Examples**

```bash
appetize screenshot
appetize screenshot home-screen
appetize screenshot ./shots/checkout.png
```

Prints `{ bytes, mimeType, output }`.

## recording start

Opens the device video stream and captures it to a file.

```bash
appetize recording start <output> [options]
```

| Argument   | Values                                                       |
| ---------- | ------------------------------------------------------------ |
| `<output>` | A path ending in `.mp4`, or no extension and `.mp4` is added |

| Flag      | Values              | Meaning                                 |
| --------- | ------------------- | --------------------------------------- |
| `--force` | — (default `false`) | Overwrite the file if it already exists |

**Examples**

```bash
appetize recording start login-flow
appetize recording start ./captures/checkout.mp4
appetize recording start login-flow --force
```

Prints `{ path, recording: true }`. `output` is required, any other extension is refused, and the directory must already exist. A relative path resolves against your shell, not the daemon's. Capture is opt-in — video is lazy device-side, so nothing streams until this runs.

## recording stop

Closes the stream and the file.

```bash
appetize recording stop
```

**Examples**

```bash
appetize recording stop
```

Prints `{ path, recording: false }`, or fails with `No video recording in progress`. A write failure is reported here rather than when it happens.

## skill install

Installs the agent skill so coding agents can drive a device.

```bash
appetize skill install [options]
```

| Flag      | Values                                                       | Meaning                                         |
| --------- | ------------------------------------------------------------ | ----------------------------------------------- |
| `--agent` | `claude`, `codex`, `copilot`, `cursor`, `agents`; repeatable | Install for these agents instead of detecting   |
| `--scope` | `project` (default), `user`                                  | Install into the project or your home directory |

**Examples**

```bash
appetize skill install
appetize skill install --scope user
appetize skill install --agent claude --agent cursor
```

Claude Code reads `.claude/skills`; Codex, Copilot and Cursor read `.agents/skills`.

## Environment variables

| Variable             | Values          | Meaning                                          |
| -------------------- | --------------- | ------------------------------------------------ |
| `APPETIZE_API_TOKEN` | `tok_…`         | Authorizes uploads, listings and session targets |
| `APPETIZE_ENDPOINT`  | An Appetize URL | Used when `--endpoint` is omitted                |

## Common failures

| Message                                          | What to check                                                                               |
| ------------------------------------------------ | ------------------------------------------------------------------------------------------- |
| `APPETIZE_API_TOKEN must be set`                 | Export a token from your organization settings.                                             |
| `No active sessions`                             | Start one; if one should be live, `daemon.log` says why it exited.                          |
| `Multiple active sessions; specify --session-id` | Pass the id of the session you mean.                                                        |
| `No session found for id X`                      | That session ended, or the id is wrong — `appetize session start` prints the id it created. |
| `Session is not ready`                           | The start hasn't finished; the phases logged by `session start` say how far it got.         |
| `No video recording in progress`                 | `recording stop` ran without a `recording start`.                                           |
| Element not found                                | Inspect again. It is off screen, covered, or the screen changed.                            |
