---
description: >-
  Give a coding agent the Appetize CLI and have it explore your app on a
  device, then write and run Playwright tests that pass.
---

# Have an agent write Playwright tests

A coding agent can write your mobile tests. You create an API token. The agent installs the CLI, uploads the app, finds what it can select on each screen, and writes the Playwright tests.

This example uses the [TODO app](https://github.com/appetizeio/todo-app) and ends with three passing tests. It works with Claude Code, Codex, Copilot, Cursor, and any other agent that runs terminal commands.

![](../.gitbook/assets/agent-writes-playwright-tests-v7.mp4)

The agent is on the left. The device, the code, and the passing tests are on the right.

## 1. Create a token

The agent can install the tools and build the project. It cannot create your API token.

Node 22 or later needs to be available. Create a token under **Organization → API Tokens**, then export it in the environment your agent uses:

```bash
export APPETIZE_API_TOKEN=tok_xxxxxxxxxxxx
```

If your Appetize URL is not `https://appetize.io`, also set `APPETIZE_ENDPOINT` to that URL.

## 2. Ask your agent

Open an empty folder in your agent and give it the task:

> Install the Appetize CLI with `npm install -g @appetize/cli`, then run `appetize skill install`.
>
> Set up a new mobile Playwright project in this folder with `npm init @appetize/playwright@latest`. If the scaffold asks for a build id or device, accept the defaults for now.
>
> Download the TODO APK from `https://github.com/appetizeio/todo-app/releases/latest/download/todo-app.apk`. Upload it with `appetize build upload ./todo-app.apk --wait`.
>
> In `playwright.config.ts`, set `use.baseURL` to `process.env.APPETIZE_ENDPOINT || 'https://appetize.io'`. Set `use.config.buildId` to the uploaded build id and `use.config.device` to `pixel7`.
>
> Use the appetize CLI to explore that build on a Pixel 7. Then write Playwright tests in `tests/` with `@appetize/playwright` for:
>
> - the Overdue filter shows overdue tasks
> - `todoapp://task/deeplink` opens the seeded task
> - `todoapp://new?title=Buy%20milk` adds a task
>
> Confirm each flow on the device before translating it into a test. Run `npx playwright test` and fix the tests until they pass. Use https://docs.appetize.io/testing/writing-tests for the test API.

Open the `viewerUrl` the agent prints to watch the device while it works.

## 3. What the agent does

1. Installs the CLI and its skill, creates the Playwright project, uploads the APK, and puts the returned build id in the configuration.
2. Starts a device and inspects each screen to find selectors and app state it can assert.
3. Confirms each requested flow on the device, translates it into a Playwright test, and runs the suite.

Exploring the running app changes how the tests are written. On the TODO app, the agent discovers:

- A fresh install opens a welcome screen, and deep links do nothing while it is up. The tests tap **Skip** first.
- **New task** is visible but missing from the UI tree, so no test can tap it. The `todoapp://new` deep link adds the task instead.
- The new task is added off screen at the bottom of the list. The test swipes up before it checks for it.

## 4. What you get

A resulting test file can look like this:

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
  3 passed
``

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
