---
description: >-
  Use the Appetize CLI to explore your app on a device, find selectors that
  work, and turn them into Playwright tests.
---

# Write Playwright tests with the CLI

Writing a mobile test is mostly finding what you can select on each screen. The CLI does that from your terminal. You start a device, inspect the screen, and try each step. Once a step works, copy it into a Playwright test.

This example uses the [TODO app](https://github.com/appetizeio/todo-app). It ends with three passing tests.

## 1. Set up

Node 22 or later.

```bash
npm install -g @appetize/cli
export APPETIZE_API_TOKEN=tok_xxxxxxxxxxxx

curl -fsSL -o todo-app.apk \
  https://github.com/appetizeio/todo-app/releases/latest/download/todo-app.apk
appetize build upload ./todo-app.apk --wait
```

Create the token under **Organization → API Tokens**. `build upload` prints an `id`. That is your build id.

If your Appetize URL is not `https://appetize.io`, also set `APPETIZE_ENDPOINT` to that URL.

## 2. Explore the app

```bash
appetize session start pixel7 YOUR_BUILD_ID
appetize inspect
```

`session start` prints a `viewerUrl`. Open it to watch the device. If the app opens on a welcome screen, run `appetize tap --select-text 'Skip'` and inspect again.

`inspect` writes `inspect.json`, the elements on screen right now. Read it for the text you can match. On the TODO list you will find `Todo`, `9 left`, the filters `All`, `Active`, `Overdue`, `Done`, and each task title.

Some things on screen are not in the tree. **New task** is visible, but it is not in `inspect.json`, so no test can tap it. The app has a deep link that adds a task instead, so the test uses that.

## 3. Try each step

Run every step with the CLI before you write it down:

```bash
appetize tap --select-text 'Overdue'
appetize inspect --select-text 'Open a task with a deep link'

appetize open 'todoapp://new?title=Buy%20milk'
appetize inspect --select-text '10 left'

appetize session stop
```

A step works when `inspect` finds the element you expect. If it says the element was not found, run `appetize inspect` without a selector and look for the text it actually shows.

The new task is added at the end of the list, off screen. That is why the check uses the `10 left` counter, not the task title.

## 4. Write the tests

Each CLI command has a Playwright equivalent:

| CLI | Playwright |
| --- | --- |
| `appetize tap --select-text 'Overdue'` | `session.tap({ element: { attributes: { text: 'Overdue' } } })` |
| `appetize open 'todoapp://…'` | `session.openUrl('todoapp://…')` |
| `appetize inspect --select-text '10 left'` | `expect(session).toHaveElement({ attributes: { text: '10 left' } })` |

In a new folder, run `npm init @appetize/playwright@latest` and enter your build id. Then replace `tests/app.spec.ts`:

{% code title="tests/app.spec.ts" %}
```typescript
import { test, expect } from '@appetize/playwright'

test.afterEach(async ({ session }) => {
    await session.reinstallApp()
})

test.beforeEach(async ({ session }) => {
    const skip = await session.findElements({ attributes: { text: 'Skip' } }, { timeout: 5000 })
    if (skip.length) await session.tap({ element: { attributes: { text: 'Skip' } } })
    await expect(session).toHaveElement({ attributes: { text: 'Todo' } })
})

test('the Overdue filter shows overdue tasks', async ({ session }) => {
    await session.tap({ element: { attributes: { text: 'Overdue' } } })
    await expect(session).toHaveElement({ attributes: { text: 'Open a task with a deep link' } })
})

test('a deep link opens a seeded task', async ({ session }) => {
    await session.openUrl('todoapp://task/deeplink')
    await expect(session).toHaveElement({ attributes: { text: 'Open a task with a deep link' } })
})

test('a deep link adds a task', async ({ session }) => {
    await session.openUrl('todoapp://new?title=Buy%20milk')
    await expect(session).toHaveElement({ attributes: { text: '10 left' } })
})
```
{% endcode %}

`reinstallApp` gives each test a fresh install, so the counter always starts at `9 left`. A fresh install sometimes opens a welcome screen first. `beforeEach` taps **Skip** when it is there.

## 5. Run them

```bash
npx playwright test
```

```
  3 passed (29.5s)
```

To run these tests on every push, see [Run Playwright in CI](../testing/continuous-integration.md).

## Let an agent do the exploring

Steps 2 and 3 are what the CLI's agent skill teaches a coding agent:

```bash
appetize skill install
```

Then ask your agent something like: *"Explore build YOUR_BUILD_ID on a Pixel 7 with the appetize CLI, then write Playwright tests with @appetize/playwright for the Overdue filter and the deep links."* It inspects, tries each step, and writes the tests from selectors it has already confirmed. See [AI Agents](../ai-agents/README.md).
