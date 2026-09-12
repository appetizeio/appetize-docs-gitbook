---
description: Getting Started with Appetize AppRecorder and Playwright
---

# Getting Started

Get a Playwright project running against your app on Appetize.

## Installation

```sh
npm init @appetize/playwright@latest
```

It asks two questions:

* Your app's **buildId** (previously known as `publicKey`). Press enter to accept `demo` and try the flow against Appetize's demo app first.
* The **default device**, picked from the devices available to your account.

{% embed url="https://cdn.jsdelivr.net/gh/appetizeio/appetize-docs-gitbook@4b0abeb/.gitbook/assets/npm-init-final.mp4" %}

To scaffold into a new folder, pass its name:

```sh
npm init @appetize/playwright@latest my-app-tests
```

{% hint style="warning" %}
Run this in a new or empty folder. In the directory it targets it empties `tests/` and deletes `tests-examples/`.
{% endhint %}

## What you get

* A Playwright project (see the [Playwright docs](https://playwright.dev/docs/intro#installing-playwright))
* The `@appetize/playwright` package
* `playwright.config.ts`, already pointed at your app and device
* `tests/app.spec.ts`, a placeholder test

{% code title="playwright.config.ts" %}
```typescript
export default defineConfig<AppetizeTestOptions>({
    testDir: './tests',
    outputDir: 'test-results/',
    timeout: 120 * 1000,
    forbidOnly: !!process.env.CI,
    retries: process.env.CI ? 3 : 0,
    reporter: 'line',

    // correlates to the number of concurrent Appetize sessions at a time
    workers: 1,
    fullyParallel: false,

    use: {
        trace: 'retain-on-failure',
        baseURL: 'https://appetize.io',

        // Appetize session configuration
        config: {
            device: 'iphone16promax',
            buildId: 'demo',
        },
    },
});
```
{% endcode %}

`use.config` is the Appetize session configuration — device, OS version, language, and anything else you can set per session. Override it for a suite with `test.use`, or per [project](https://docs.appetize.io/testing/projects).

## Write a test

Update `tests/app.spec.ts` to match something in your own app:

```javascript
import { test, expect } from '@appetize/playwright'

test('example test', async ({ session }) => {
    await expect(session).toHaveElement({
        attributes: {
            // replace with the text of an element that appears in your app
            text: 'Hello world'
        }
    })
})
```

## Run it

```bash
npx playwright test --headed

# or, headlessly

npx playwright test
```

When a test fails, Appetize attaches the device screenshot, the full UI hierarchy and the session details to the result — see [Trace Viewer](https://docs.appetize.io/testing/trace-viewer).
