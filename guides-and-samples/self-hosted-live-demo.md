---
description: >-
  Connect to your self-hosted Appetize deployment, drive the sample TODO app
  with the CLI, run the same checks in Playwright, and keep the test results.
---

# Run the TODO app

Use the sample [TODO app](https://github.com/appetizeio/todo-app) to try your self-hosted deployment from your own machine. You connect the CLI, drive the app, run those checks in Playwright, and save the test results from CI.

Do the steps in order. Each step ends with what you should see. Stop there if it does not match.

You need three values:

| Value | What to put | Where you get it |
| --- | --- | --- |
| `APPETIZE_ENDPOINT` | `https://appetize.example.com` | The host you open in a browser for this deployment |
| `APPETIZE_API_TOKEN` | `tok_…` | **Organization → API Tokens** on that same host |
| `BUILD_ID` | the id returned when you upload | Step 2 |

Playwright and the CLI use this host. A self-hosted deployment does not use `appetize.io`.

## 1. Connect the CLI

Install [Node 22](https://nodejs.org/) or later, then install the CLI and point it at your deployment:

```bash
npm install -g @appetize/cli

export APPETIZE_ENDPOINT=https://appetize.example.com
export APPETIZE_API_TOKEN=tok_xxxxxxxxxxxx

appetize build list
```

You should see a JSON list of the apps on your deployment. An empty list is fine if you have not uploaded one yet.

If the command hangs or the connection is refused, this machine cannot reach `APPETIZE_ENDPOINT`. Check DNS, the certificate, and that HTTPS is allowed from your machine before you continue.

## 2. Upload the sample app

Download the APK:

```bash
curl -fsSL -o todo-app.apk \
  https://github.com/appetizeio/todo-app/releases/latest/download/todo-app.apk
```

Upload `todo-app.apk` from the upload page on your deployment. If that page cannot reach GitHub, upload a copy of the file you already have on disk.

Copy the build id from the app page. The upload API calls this field `publicKey`. It is the same value.

```bash
export BUILD_ID=your_build_id
appetize build list
```

You should see that id in the list. The app is the TODO app, package `io.appetize.todo`.

## 3. Drive the app

List the Android devices on your deployment and copy one id. The examples below use `pixel7`. Use an id your list actually prints.

```bash
appetize device list --platform android
export DEVICE_ID=pixel7

appetize session start "$DEVICE_ID" "$BUILD_ID" --session-id todo-demo
```

You should see the startup phases on screen, ending in `ready`: `requesting`, `starting`, `downloadingApp`, `installingApp`, `launchingApp`. The first start is the slow one, because the device still has to download the APK. `queued` means every device slot is in use. Stop the other session, or wait.

The command also prints a `viewerUrl` such as `http://127.0.0.1:52518/`. Open it. You should see the TODO list: the title is **Todo**, the button is **New task**, and one row says **Open a task with a deep link**.

A blank page with a session that reached `ready` means WebSockets from your machine to the deployment are blocked. You can still continue. `inspect` and `screenshot` talk to the session directly.

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

You should get `demo/list.png`, `demo/task.png`, and `demo/todo.mp4`. The second screenshot is the overdue task. In the viewer, the **Overdue** filter is selected and that row is on screen.

`inspect` prints the text on screen. `tap` uses that text. The PNG and MP4 are the record of what the device showed. These are the same commands an agent runs.

Stop the session before you run the tests. A deployment with one concurrent session cannot start the Playwright session while this one is still open.

```bash
appetize session stop
```

## 4. Run the same checks in Playwright

In an empty folder, create a Playwright project:

```bash
mkdir todo-tests
cd todo-tests
npm init @appetize/playwright@latest
```

Press Enter when it asks for a build id, and accept any device. You replace both answers in the next file. The command writes `playwright.config.ts` and `tests/app.spec.ts`.

Replace `playwright.config.ts` with:

{% code title="playwright.config.ts" %}
```typescript
import { defineConfig } from '@playwright/test'
import { type AppetizeTestOptions } from '@appetize/playwright'

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
            device: process.env.DEVICE_ID,
            buildId: process.env.BUILD_ID,
        },
    },
})
```
{% endcode %}

`baseURL` is your deployment. If `APPETIZE_ENDPOINT` is unset, the tests open `https://appetize.io` instead. `workers: 1` keeps a single session. Add workers only up to the number of sessions your deployment allows.

Replace `tests/app.spec.ts` with the test below. Delete any other file in `tests/`. A leftover sample test still runs, and it looks for text this app does not have.

{% code title="tests/app.spec.ts" %}
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

`session` is the device, in the same way `page` is the browser in a normal Playwright test. `openUrl` sends `todoapp://task/deeplink`, which this app handles by scrolling to a seeded row. Tasks stay on the device after a test, so `reinstallApp` gives the next test a fresh install.

`APPETIZE_ENDPOINT`, `BUILD_ID`, and `DEVICE_ID` still need to be exported in this terminal. Then run:

```bash
npx playwright test --headed
```

You should see two passing tests. With `--headed`, the device is on screen while they run. Drop `--headed` when you want the same run without a window.

Open the report:

```bash
npx playwright show-report
```

A failure writes `test-results/<test-name>/`. That folder holds a screenshot of the device, a JSON file of every element on screen, and the session record. Open the trace with:

```bash
npx playwright show-trace test-results/<test-name>/trace.zip
```

Read the UI attachment first. It is the text that was actually on screen, which is the text the next selector should use. The trace also contains the session token, so keep the report private.

## 5. Keep the results in CI

Run the same project from a workflow. The job runner has to reach your deployment, the same way your machine did in step 1.

Store these as secrets:

| Secret | Value |
| --- | --- |
| `APPETIZE_ENDPOINT` | The host from step 1 |
| `APPETIZE_API_TOKEN` | The token from step 1 |
| `APPETIZE_API_ORIGIN` | The API host for your installation. Cloud docs use `https://api.appetize.io`. Use the host for your installation. |
| `BUILD_ID` | The build id from step 2 |
| `DEVICE_ID` | The device id from step 3 |

This workflow does two different uploads. The `curl` step sends a new APK to your deployment and keeps the same `BUILD_ID`. The last step uploads the Playwright report to the CI run, so you can download it when a test fails.

The Playwright files from step 4 are the repository root in this example: `playwright.config.ts`, `tests/app.spec.ts`, `package.json`, and `package-lock.json`.

```yaml
name: todo

on:
  workflow_dispatch:

jobs:
  test:
    runs-on: ubuntu-latest
    env:
      APPETIZE_ENDPOINT: ${{ secrets.APPETIZE_ENDPOINT }}
      APPETIZE_API_TOKEN: ${{ secrets.APPETIZE_API_TOKEN }}
      APPETIZE_API_ORIGIN: ${{ secrets.APPETIZE_API_ORIGIN }}
      BUILD_ID: ${{ secrets.BUILD_ID }}
      DEVICE_ID: ${{ secrets.DEVICE_ID }}
    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-node@v4
        with:
          node-version: 22

      - run: npm install
      - run: npx playwright install --with-deps chromium

      - name: Download the sample APK
        run: |
          curl -fsSL -o todo-app.apk \
            https://github.com/appetizeio/todo-app/releases/latest/download/todo-app.apk

      - name: Update the app on your deployment
        run: |
          curl -fsS -X POST "$APPETIZE_API_ORIGIN/v1/apps/$BUILD_ID" \
            -H "X-API-KEY: $APPETIZE_API_TOKEN" \
            -F "file=@todo-app.apk" \
            -F "platform=android"

      - name: Run tests
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

After a run, open the job and download **playwright-results**. `playwright-report/` is the HTML report. `test-results/` holds the traces and the per-test screenshot, UI hierarchy, and session record.

The APK is the app under test. The report is how you tell what the test saw. Updating the APK does not store the report, and uploading the report does not change the app.

If the runner cannot download from GitHub, build the APK in the job, or pass in an APK you already produced, and point the `curl` upload at that file. The [direct file upload](../rest-api/v1/direct-file-uploads.md) reference uses the same request against `https://api.appetize.io`.

## When a step does not match

| What you see | What to check |
| --- | --- |
| `build list` hangs or the connection is refused | DNS, the certificate, and HTTPS from this machine to `APPETIZE_ENDPOINT`. |
| The viewer stays blank after `ready` | WebSockets from this machine to the deployment. `inspect` and `screenshot` still work. |
| The log stays on `queued` | Another session is using the only free device. Run `appetize session stop`, then start again. |
| `Element not found` | The row is off screen. Run `appetize inspect` again, or `appetize swipe --direction up`, and tap the text it prints. |
| The deep link test does not show the seeded task | The app was already installed with older data. `reinstallApp` in the test puts the next run on a fresh install. |
| Playwright opens `appetize.io` | `APPETIZE_ENDPOINT` was empty, so `baseURL` fell back to the cloud. Export it in the same terminal. |
| The Playwright session never starts | The CLI session from step 3 is still open, or `BUILD_ID` is empty. |
