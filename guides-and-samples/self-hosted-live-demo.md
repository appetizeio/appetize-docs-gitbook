---
description: >-
  A 20-minute call script for a self-hosted Appetize deployment. Connect the
  CLI, drive the TODO app, run the same flow in Playwright, and keep the CI artifacts.
---

# Self-hosted live demo

Send this page ahead of a call, then follow it on screen. It takes about 20 minutes and uses the public [TODO app](https://github.com/appetizeio/todo-app), a small Android app with no backend.

The customer sees three things, on their own deployment:

1. The CLI connects to their host and drives the app.
2. A Playwright test does the same work through the `session` fixture.
3. CI keeps two different outputs: the APK on Appetize, and the test report in the pipeline.

Self-hosted and Private Cloud look the same from here. Both are a dedicated deployment. The CLI and Playwright only need that deployment's URL and an API token. What changes is the hostname, and that the customer runs the host.

## Before the call

Do this on the deployment you will demo. A live upload or a first `npm install` is a bad use of the 20 minutes.

* Confirm the laptop and the CI runner can open the deployment over HTTPS, and that WebSockets are not blocked. A blank device usually means the socket never connected.
* Create an API token on that deployment.
* Upload [todo-app.apk](https://github.com/appetizeio/todo-app/releases/latest/download/todo-app.apk) once, from the deployment's upload page or with the [direct file upload](../rest-api/v1/direct-file-uploads.md) call. If the environment cannot reach GitHub, upload the APK file from disk. Write down the `buildId`.
* Install the CLI (`Node 22+`) and scaffold the Playwright project below, so both already run against that `buildId`.
* Pick a device with `appetize device list --platform android`. The commands below use `pixel7`. Swap in an id that this deployment actually lists.

```bash
export APPETIZE_ENDPOINT=https://appetize.customer.example
export APPETIZE_API_TOKEN=tok_xxxxxxxxxxxx
```

`APPETIZE_ENDPOINT` is the deployment's own URL. There is no separate discovery step. Playwright uses the same URL as `baseURL`.

## 1. Show that the CLI is on their host (5 min)

```bash
appetize build list
appetize device list --platform android
```

The build list should contain the TODO app you uploaded. If it lists cloud apps, or the request never returns, the endpoint or the token is wrong. Fix that before starting a session.

```bash
appetize session start pixel7 "$BUILD_ID" --session-id todo-demo
```

`session start` prints a local `viewerUrl`. Open it and leave it on screen. The page is the device, and input on it goes to the device, so you can point at what the next command does.

Progress is printed on stderr: `requesting`, `queued`, `starting`, `downloadingApp`, `installingApp`, `launchingApp`, `ready`. On a first run, `downloadingApp` is the long one.

## 2. Drive the app from the terminal (5 min)

The list is on screen. The title is `Todo`, and the button is `New task`. Seeded rows include `Open a task with a deep link`.

```bash
mkdir -p demo
appetize inspect --select-text 'Todo' --pretty
appetize screenshot ./demo/list.png
appetize recording start ./demo/todo
appetize tap --select-text 'Overdue'
appetize tap --select-text 'Open a task with a deep link'
appetize screenshot ./demo/task.png
appetize recording stop
```

Say this while it runs: the CLI is not a test framework. `inspect` is how you see the screen, a selector is how you act, and the PNG and MP4 are how you show what happened. The same commands are what an agent runs.

`recording start` needs the directory to exist already. `session stop` at the end of the call releases the device.

The session JSON also includes an `adbSerial`. That is a normal Android device for as long as the session lives:

```bash
adb connect 127.0.0.1:57275
adb shell am start -a android.intent.action.VIEW -d "todoapp://task/deeplink"
```

Use the serial from this session, not the port in the example. `todoapp://task/deeplink` scrolls to the seeded task on a fresh install.

## 3. The same flow as a Playwright test (5 min)

`npm init @appetize/playwright@latest` in an empty folder writes a project whose fixture is `session`. Point it at the same host and build:

{% code title="playwright.config.ts" %}
```typescript
import { defineConfig } from '@playwright/test'
import { AppetizeTestOptions } from '@appetize/playwright'

export default defineConfig<AppetizeTestOptions>({
    testDir: './tests',
    outputDir: 'test-results/',
    timeout: 120 * 1000,
    workers: 1,
    fullyParallel: false,
    reporter: [['line'], ['html', { open: 'never' }]],
    use: {
        trace: 'retain-on-failure',
        baseURL: process.env.APPETIZE_ENDPOINT,
        config: {
            device: 'pixel7',
            buildId: process.env.BUILD_ID,
        },
    },
})
```
{% endcode %}

`workers: 1` is one Appetize session. Extra workers queue once they pass the deployment's concurrency.

{% code title="tests/todo.spec.ts" %}
```typescript
import { test, expect } from '@appetize/playwright'

test.afterEach(async ({ session }) => {
    await session.reinstallApp()
})

test('the list is on screen', async ({ session }) => {
    await expect(session).toHaveElement({ attributes: { text: 'Todo' } })
    await expect(session).toHaveElement({ attributes: { text: 'New task' } })
})

test('a deep link opens a seeded task', async ({ session }) => {
    await session.openUrl('todoapp://task/deeplink')
    await expect(session).toHaveElement({
        attributes: { text: 'Open a task with a deep link' },
    })
})
```
{% endcode %}

Tasks persist inside a session, so `reinstallApp` puts the next test back on a fresh install. Run it headed when you want the device on screen:

```bash
npx playwright test --headed
```

A failure writes three attachments into `test-results/`: a screenshot, the UI hierarchy, and the session record. Open the trace with:

```bash
npx playwright show-trace test-results/<test-name>/trace.zip
```

The hierarchy is the one to open on the call. It is the list of text actually on screen, which is what you match next. Traces include the session token. Treat them as private once the app is the customer's.

## 4. Where the two artifacts go (5 min)

Walk this job from top to bottom. Do not run it live unless the runner is already able to reach the deployment.

```yaml
jobs:
  todo:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Upload the APK to Appetize
        env:
          APPETIZE_API_TOKEN: ${{ secrets.APPETIZE_API_TOKEN }}
        run: |
          curl -fsS -X POST "$APPETIZE_API_ORIGIN/v1/apps/$BUILD_ID" \
            -H "X-API-KEY: $APPETIZE_API_TOKEN" \
            -F "file=@app-release.apk" \
            -F "platform=android"

      - name: Run Playwright
        env:
          APPETIZE_ENDPOINT: ${{ secrets.APPETIZE_ENDPOINT }}
          APPETIZE_API_TOKEN: ${{ secrets.APPETIZE_API_TOKEN }}
          BUILD_ID: ${{ secrets.BUILD_ID }}
        run: npx playwright test

      - name: Upload the test report
        if: ${{ !cancelled() }}
        uses: actions/upload-artifact@v4
        with:
          name: playwright-results
          path: |
            playwright-report/
            test-results/
```

Two uploads, two places:

| Output | Where it goes | What it is for |
| --- | --- | --- |
| APK | The deployment, addressed by `buildId` | The app under test. Updating it is how the next run picks up a new build. |
| `playwright-report/` and `test-results/` | The CI run, as a job artifact | The HTML report, traces, screenshots, UI hierarchy, and session record. Download these when a test fails. |

The public [direct upload](../rest-api/v1/direct-file-uploads.md) examples call `https://api.appetize.io`. On a self-hosted deployment, `$APPETIZE_API_ORIGIN` is the API origin you were given for that install. It is not `api.appetize.io`.

`$BUILD_ID` in the `curl` line updates the app you already uploaded. A first upload is `POST` to `/v1/apps` with no id, and the response is the `buildId` you then store as a secret.

## If the call stalls

| What you see | What to say |
| --- | --- |
| `build list` hangs or refuses the connection | The runner cannot reach `APPETIZE_ENDPOINT`. Check DNS, TLS, and the firewall before retrying the demo. |
| Viewer stays blank | The streaming socket is blocked. The session can still be healthy. `inspect` and `screenshot` do not need the viewer. |
| stderr sits on `queued` | The deployment is at its concurrency limit. Stop the other session, or wait. |
| `Element not found` | The row is off screen. `inspect` again, or `swipe --direction up`, then tap the text it prints. |
| Deep link does nothing | The install is not fresh, or another app claimed the scheme. `reinstallApp` in Playwright, or a new session for the CLI. |

## Leave this with them

* This page.
* The [TODO app](https://github.com/appetizeio/todo-app), including the deep-link table in its README.
* [CLI getting started](../ai-agents/getting-started.md) and [Playwright getting started](../testing/getting-started.md).
* The `buildId`, the endpoint, and where the API token is stored. Those three are the whole connection.
