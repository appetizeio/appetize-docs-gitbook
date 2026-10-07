---
description: >-
  Give a coding agent the Appetize CLI and have it explore your app on a
  device, then write and run Playwright tests that pass.
---

# Have an agent write Playwright tests

A coding agent can write your mobile tests. With the Appetize CLI, it runs your app on a device, finds what it can select on each screen, and tries every step. Then it writes the Playwright tests and runs them until they pass.

This example uses the [TODO app](https://github.com/appetizeio/todo-app) and ends with three passing tests. It works with Claude Code, Codex, Copilot, Cursor, and any other agent that runs terminal commands.

![](../.gitbook/assets/agent-writes-playwright-tests-v2.mp4)

The agent is on the left. The device, the code, and the passing tests are on the right.

## 1. Set up

Node 22 or later. In a new folder:

```bash
npm install -g @appetize/cli
export APPETIZE_API_TOKEN=tok_xxxxxxxxxxxx

npm init @appetize/playwright@latest
appetize skill install
```

Create the token under **Organization → API Tokens**. If your Appetize URL is not `https://appetize.io`, also set `APPETIZE_ENDPOINT` to that URL.

`npm init @appetize/playwright` creates the Playwright project. Press Enter at the build id prompt. You will set it in the next step. `skill install` teaches your agent the CLI.

Upload the app:

```bash
curl -fsSL -o todo-app.apk \
  https://github.com/appetizeio/todo-app/releases/latest/download/todo-app.apk
appetize build upload ./todo-app.apk --wait
```

Copy the `id` it prints. That is your build id.

## 2. Ask your agent

Open your agent in that folder and give it the task:

> Use the appetize CLI to explore build `YOUR_BUILD_ID` on a Pixel 7. Then write Playwright tests in `tests/` with `@appetize/playwright` for:
>
> - the Overdue filter shows overdue tasks
> - `todoapp://task/deeplink` opens the seeded task
> - `todoapp://new?title=Buy%20milk` adds a task
>
> Set the build id in `playwright.config.ts`. Try every step with the CLI before you write it. Run `npx playwright test` and fix the tests until they pass. Use https://docs.appetize.io/testing/writing-tests for the test API.

Open the `viewerUrl` the agent prints to watch the device while it works.

## 3. What the agent does

1. Starts a device with `appetize session start` and runs `appetize inspect` to read what is on screen.
2. Tries each step with `appetize tap` and `appetize open`, and checks the result with `inspect`.
3. Writes the tests from the steps that worked, then runs them.

Trying each step first is what makes the tests pass. On the TODO app, the agent finds:

- A fresh install opens a welcome screen, and deep links do nothing while it is up. The tests tap **Skip** first.
- **New task** is visible but missing from the UI tree, so no test can tap it. The `todoapp://new` deep link adds the task instead.
- The new task is added off screen at the bottom of the list. The test swipes up before it checks for it.

## 4. What you get

This is the file an agent wrote from the prompt above:

{% code title="tests/app.spec.ts" %}
```typescript
import { test, expect } from '@appetize/playwright'

test.afterEach(async ({ session }) => {
    await session.reinstallApp()
})

test.beforeEach(async ({ session }) => {
    const skip = await session.findElements(
        { attributes: { text: 'Skip' } },
        { timeout: 5000 }
    )
    if (skip.length) {
        await session.tap({ element: { attributes: { text: 'Skip' } } })
    }
})

test('Overdue filter shows overdue tasks', async ({ session }) => {
    await session.tap({ element: { attributes: { text: 'Overdue' } } })

    await expect(session).toHaveElement({
        attributes: { text: 'Open a task with a deep link' },
    })
    await expect(session).toHaveElement({
        attributes: { text: 'Review the Q3 release notes' },
    })
    await expect(session).not.toHaveElement(
        { attributes: { text: 'Send the standup summary' } },
        { timeout: 1000 }
    )
})

test('todoapp://task/deeplink opens the seeded task', async ({ session }) => {
    await session.openUrl('todoapp://task/deeplink')

    await expect(session).toHaveElement({
        attributes: { text: 'Open a task with a deep link' },
    })
})

test('todoapp://new?title=Buy%20milk adds a task', async ({ session }) => {
    await session.openUrl('todoapp://new?title=Buy%20milk')

    await session.swipe({
        position: { x: '50%', y: '50%' },
        gesture: 'up',
    })

    await expect(session).toHaveElement({
        attributes: { text: 'Buy milk' },
    })
})
```
{% endcode %}

Your agent's file will be different, but it should test the same steps. Run it yourself:

```bash
npx playwright test
```

```
  3 passed (15.5s)
```

To run them on every push, see [Run Playwright in CI](../testing/continuous-integration.md).

## Doing it by hand

The agent only runs CLI commands, so you can run the same steps yourself. Each command maps to one Playwright call:

| CLI | Playwright |
| --- | --- |
| `appetize tap --select-text 'Overdue'` | `session.tap({ element: { attributes: { text: 'Overdue' } } })` |
| `appetize open 'todoapp://…'` | `session.openUrl('todoapp://…')` |
| `appetize swipe --direction up` | `session.swipe({ position: { x: '50%', y: '50%' }, gesture: 'up' })` |
| `appetize inspect --select-text 'Buy milk'` | `expect(session).toHaveElement({ attributes: { text: 'Buy milk' } })` |

See [AI Agents](../ai-agents/README.md) for every CLI command.
