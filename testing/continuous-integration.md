---
description: >-
  Run an Appetize Playwright project in CI and keep the HTML report, traces,
  and screenshots.
---

# Run Playwright in CI

CI runs the same `npx playwright test` command you run on your machine. This page covers the Appetize settings, and how to keep the report when a test fails.

Playwright's own [CI guide](https://playwright.dev/docs/ci) covers the runner, retries, and reporters.

## 1. Point the project at your app

{% code title="playwright.config.ts" %}
```typescript
import { defineConfig } from '@playwright/test'
import { type AppetizeTestOptions } from '@appetize/playwright'

export default defineConfig<AppetizeTestOptions>({
    testDir: './tests',
    outputDir: 'test-results/',
    timeout: 120 * 1000,
    workers: 1,
    reporter: [['line'], ['html', { open: 'never' }]],
    use: {
        trace: 'retain-on-failure',
        baseURL: 'https://appetize.io',
        config: {
            buildId: process.env.BUILD_ID,
            device: 'pixel7',
        },
    },
})
```
{% endcode %}

`buildId` is the app you uploaded. `workers: 1` is one device session. Raise it only up to the number of sessions your account allows.

Set `baseURL` to your Appetize URL when it is not `https://appetize.io`.

## 2. Add your tests

Tests use the `session` fixture, which is the device. If you do not have tests yet, [Have an agent write Playwright tests](../guides-and-samples/test-with-the-cli.md) creates three for the TODO app. Commit `playwright.config.ts`, `tests/`, `package.json`, and `package-lock.json`.

## 3. Run the job and upload the report

Store `BUILD_ID` as a secret. The job runner must be able to open `baseURL`.

```yaml
name: playwright

on:
  workflow_dispatch:

jobs:
  test:
    runs-on: ubuntu-latest
    env:
      BUILD_ID: ${{ secrets.BUILD_ID }}
    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-node@v4
        with:
          node-version: 22

      - run: npm install
      - run: npx playwright install --with-deps chromium
      - run: npx playwright test

      - name: Upload the test report
        if: ${{ !cancelled() }}
        uses: actions/upload-artifact@v4
        with:
          name: playwright-results
          path: |
            playwright-report/
            test-results/
```

`if: ${{ !cancelled() }}` uploads the report when the tests fail. A failed run is hard to read without it.

Download **playwright-results** from the job:

| Path | What it is |
| --- | --- |
| `playwright-report/` | The HTML report. Open it in a browser. |
| `test-results/` | The trace, the device screenshot, the UI hierarchy, and the session record. |

```bash
npx playwright show-trace test-results/<test-name>/trace.zip
```

See [Trace Viewer](trace-viewer.md). The report contains a session token, so keep the artifact private.

This upload is the test report. It does not upload your app. A new build gets a new `buildId` from `appetize build upload` or the [upload API](../rest-api/v1/direct-file-uploads.md). Put that id in the `BUILD_ID` secret when you want CI to test it.
