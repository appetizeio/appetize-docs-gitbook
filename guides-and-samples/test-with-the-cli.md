---
description: >-
  Give a coding agent the Appetize CLI and have it explore your app on a
  device, then write and run Playwright tests that pass.
---

# Have an agent write Playwright tests

A coding agent can write your mobile tests. You create an API token. The agent installs the CLI, uploads the app, finds what it can select on each screen, and writes the Playwright tests.

This example uses the [TODO app](https://github.com/appetizeio/todo-app). It works with Claude Code, Codex, Copilot, Cursor, and any other agent that runs terminal commands.

## 1. Create a token

The agent can install the tools and build the project. It cannot create your API token.

Node 22 or later needs to be available. Create a token under **Organization → API Tokens**, then export it in the environment your agent uses:

```bash
export APPETIZE_API_TOKEN=tok_xxxxxxxxxxxx
```

If your Appetize URL is not `https://appetize.io`, also set `APPETIZE_ENDPOINT` to that URL.

## 2. Ask your agent

Open an empty folder in your agent and give it the task:

> Install the Appetize CLI and its skill. The CLI is documented at https://docs.appetize.io/ai-agents/getting-started.
>
> Create Playwright tests for the TODO app with `@appetize/playwright`. Upload the app with the Appetize CLI.
>
> Cover these flows:
>
> - the Overdue filter
> - opening a task with `todoapp://task/deeplink`
> - adding a task with `todoapp://new`
>
> Run the tests until they pass. Use https://docs.appetize.io/testing/writing-tests for the test API.

Open the `viewerUrl` the agent prints to watch the device while it works.

## 3. What the agent does

1. Installs the CLI and its skill, creates the Playwright project, and uploads the app.
2. Drives the three flows on a device.
3. Writes a test for each flow and runs the suite.

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

Your agent's file will be different, but it should cover the same three flows.

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
