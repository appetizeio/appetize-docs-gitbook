# Trace Viewer

The [Playwright Trace Viewer](https://playwright.dev/docs/trace-viewer-intro) records what happened during a test so you can step back through it afterwards. Projects created with `npm init @appetize/playwright` already keep a trace whenever a test fails:

{% code title="playwright.config.ts" %}
```typescript
use: {
    trace: 'retain-on-failure',
}
```
{% endcode %}

Use `'on'` to keep one for every test, or `'on-first-retry'` on CI.

## Opening a trace

```bash
npx playwright show-trace test-results/<test-name>/trace.zip
```

From CI, download the artifact and open it the same way, or drop the file on [trace.playwright.dev](https://trace.playwright.dev).

## What you get for a mobile test

Trace Viewer was built for web testing, so two panels describe the page hosting the device rather than your app: **Network** lists the embed page's requests, not your app's traffic, and **Console** and **Source** belong to the test runner. Everything else applies:

| Panel                    | For an Appetize test                                         |
| ------------------------ | ------------------------------------------------------------ |
| **Filmstrip and player** | The device screen across the whole run — scrub to any moment |
| **Actions**              | Every Appetize action with how long it took                  |
| **Errors**               | The assertion that failed                                    |
| **Attachments**          | Appetize's own per-test artifacts, below                     |

## Appetize attachments

Each test attaches three files, visible under **Attachments** and in `test-results/<test-name>/attachments`:

| Attachment   | Contents                                                               |
| ------------ | ---------------------------------------------------------------------- |
| `screenshot` | Full-resolution capture of the device                                  |
| `ui`         | The complete UI hierarchy — every element on screen and its attributes |
| `session`    | The session's resolved device config, and its token                    |

When a selector fails, `ui` is usually the quickest fix: it is the list of what was actually on screen, so you can see what to match instead.

## The session token

`session` carries the token for the exact Appetize session the test ran on:

```json
{
  "path": "https://<device>.appetize.io",
  "token": "<session token>",
  "config": { "device": "iphone17pro", "osVersion": "26.0", "platform": "ios" }
}
```

That token is worth keeping hold of:

* **Send it to us.** If a test fails for a reason that looks like Appetize rather than your app, the token lets support look at that exact session.
* **Find the session.** `GET /v2/sessions?sessionToken=<token>` returns just that session — an unknown token comes back as an empty list rather than an error. You can also match the `sessionToken` column in the Session History export. The search box on [Session History](https://appetize.io/sessions) matches app id, name and user — not the token.
* **Download its logs.** If the session captured app logs or network traffic, they are attached to it: `GET /v2/sessions/{sessionToken}/attachment?type=debug-logs` or `type=network-captures`. These are the same files behind the **Files** column on Session History. A session that did not capture that artifact returns `404`.

App logs and network captures only exist if the session asked for them, which you can turn on per project:

```typescript
use: {
    config: {
        buildId: '<your build id>',
        debug: true,          // capture app logs
        proxy: 'intercept',   // capture network traffic
    },
}
```

{% hint style="warning" %}
A trace contains video of your app and the session token. Treat trace artifacts from CI as private.
{% endhint %}
